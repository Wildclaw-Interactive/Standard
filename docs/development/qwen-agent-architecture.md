# Qwen Agent Architecture

> Private developer documentation for Standard Studio `0.1.2-alpha`.

The Qwen Agent deliberately does **less** than a general autonomous coding system. Its design goal is predictable completion of ordinary Standard project tasks without open-ended executor loops.

## Pipeline

```text
User request
   ↓
Planner             1 model turn
   ↓
Worker              max 12 actions
   ↓
Deterministic quick checks
   ↓ failure
Bounded repair      max 4 actions, then stop if still invalid
   ↓ pass
Real Standard build
   ↓ failure
Bounded build repair max 4 actions, then stop if still invalid
   ↓ pass
Evaluator           1 model turn
   ↓ optional repair
Final repair        max 3 actions
   ↓
Final deterministic validation
```

There is also a hard cap of **24 model turns for the entire task**. A task that cannot be validated inside those bounds is reported as stopped/unsuccessful rather than being allowed to loop.

## Tool contract

Qwen receives only these actions:

```text
list_files
read_file
write_file
delete_file
check_project
finish
```

`write_file` always supplies the complete contents of one file. The preferred model protocol is intentionally line-oriented (`ACTION`, optional `PATH`, and fenced `CONTENT`) so whole Standard files do not need to be JSON-escaped. The parser still accepts compact JSON actions as a fallback. There is intentionally no search/replace patch language, shell, arbitrary process tool, task-result recall tool, source-control tool, or recursive sub-agent tool in the first implementation.

The file layer allows only:

```text
.standard
.standardui
.standardproject
```

All paths are project-relative and canonicalized before use. Escaping the active project root is rejected.

## Context

Every planner/worker/evaluator turn receives the compact built-in `StandardAgentCheatSheet`. It is source-controlled with Studio and should be updated whenever public Standard syntax changes.

Project context stays bounded:

- project manifest when present;
- Standard project file list;
- active file contents (bounded);
- last tool result;
- short recent action journal;
- changed-file contents for final evaluation (bounded).

The model is expected to use `read_file` only when it actually needs another file's contents.

## Validation authority

Qwen never decides whether Standard code parses. `StandardAgentTools` runs the real Standard frontend, Standard UI parser/binder, and final `StandardBuildService` build. Deterministic diagnostics are authoritative.

The evaluator is only a requirement-completeness check after the deterministic build has passed.

## Loop protection

The implementation has several independent guards:

- hard whole-task model-turn limit;
- phase-specific action limits;
- maximum two malformed tool responses in a worker phase;
- stop after four actions with no concrete progress;
- reject repeated identical whole-file writes;
- at most one evaluator-requested repair phase;
- no evaluator-on-evaluator cycle.

Do not remove these casually. Reliability is a product feature of Standard Studio's agent mode.

## Local model/runtime

The first integration is Qwen-only and uses a pinned Qwen3.5 9B Q4_K_M GGUF with a pinned llama.cpp build. Studio downloads them after explicit user confirmation and verifies SHA-256 before installation.

The model is not loaded merely because Studio starts. Once installed, the toolbar exposes **Load Qwen AI**; the Qwen panel becomes available only after llama-server reports healthy and the model is loaded.

The local runtime binds only to `127.0.0.1` and is stopped when Standard Studio exits. CUDA launches use a conservative context/batch profile and leave llama.cpp's device-memory fitter enabled so 8 GB-class systems can offload only the layers that fit instead of failing an all-or-nothing full-offload request.
