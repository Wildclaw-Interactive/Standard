# Qwen Agent

> **Applies to:** Standard `0.1.2-alpha`

Standard Studio includes an optional local **Qwen Agent** for building and editing Standard projects from natural-language requests.

The agent is intentionally Standard-specific. Its file tools can modify only:

```text
.standard
.standardui
.standardproject
```

It cannot use its coding tools to write C#, XAML, project-system files, scripts, or files outside the active project folder.

## Install on first use

Qwen is **not bundled** inside the Standard Studio download.

In Standard Studio, click **Install Qwen AI**. Standard Studio will ask for confirmation and then automatically download:

- the pinned Qwen3.5 9B GGUF model;
- the pinned llama.cpp local inference engine; and
- a pinned Windows x64 llama.cpp runtime (CUDA acceleration on NVIDIA systems, CPU fallback otherwise).

The first download is roughly 6 GB. Files are stored under your local Standard application-data folder rather than inside each project.

Downloads can resume after interruption and are SHA256-verified before installation. Standard Studio preserves `.part` downloads across cancellation/crashes; if a previous run already downloaded the complete model, the next run verifies and promotes that file instead of downloading it again. Temporary Windows sharing violations from scanners/indexers are retried rather than treated as corruption. Once installed, Standard Studio shows **Load Qwen AI** on later launches but does not consume several gigabytes of RAM/VRAM until you choose to load it. The Agent panel is made available only after the local model reports that it is loaded and ready.

## Using the Agent

Open a Standard project folder, or even an empty folder you want Qwen to turn into a Standard project. Open the **Qwen Agent** panel and describe the result you want.

Examples:

```text
Make a calculator app with a Standard UI and four basic operations.
```

```text
Add a difficulty dropdown to this project and show the selected difficulty on screen.
```

```text
Turn this empty folder into a small notes app using Standard UI.
```

The agent is project-aware and receives the current project structure, manifest, active file, and an always-available compact Standard language/UI cheat sheet. It does not need to reread the documentation for ordinary syntax on every task. The `0.1.2-alpha` cheat sheet includes one-line and multi-line `Note:` comments, loop control, compound assignment, and runnable UI startup rules.

For generated UI applications, the cheat sheet and worker instructions explicitly require the entry `.standard` file to `Show interface` for the intended startup UI. Standard also auto-starts the only UI in a simple `Auto`/`Desktop` project as a safety net, while multi-window projects must choose their startup interface explicitly.

## Bounded workflow

The workflow is deliberately smaller than a general-purpose autonomous coding agent:

```text
Planner
  ↓
Worker
  ↓
Standard quick checks
  ↓
real Standard build
  ↓
Evaluator
```

The worker has only six simple actions:

```text
list_files
read_file
write_file
delete_file
check_project
finish
```

`write_file` writes one complete Standard file. Tool actions use a deliberately tiny line-oriented protocol internally (`ACTION`, `PATH`, and raw `CONTENT`) so Qwen does not need to construct complicated patch objects or escape an entire source file into JSON. The entire file body follows `CONTENT:`; Markdown fences are optional and tolerated rather than required. Small JSON actions are also accepted for resilience.

The agent is limited to a fixed number of model turns and repair actions. Repeated no-progress actions and repeated identical writes are stopped by loop guards rather than allowing an open-ended executor loop.

Before an existing project file is changed or deleted for the first time in a task, Standard Studio stores a backup under:

```text
.standard/agent-backups/
```

That directory is outside normal Standard project compilation.

## Validation

After implementation, Standard Studio performs deterministic validation itself rather than asking Qwen to decide whether code parses:

1. Standard language frontend checks;
2. Standard UI parser/binder checks;
3. a real Standard project build;
4. one bounded evaluator pass for user-request completeness.

If a deterministic check fails, Qwen receives the concrete diagnostic and gets one small repair phase. If the bounded repair still fails, the task stops and is **not** reported as successful.

## Privacy and network behavior

Inference runs against the local Qwen model after installation. The agent does not require a cloud AI account or API key.

Network access is used during initial model/runtime installation. Standard projects are not uploaded to a cloud AI service by this feature.

## Current platform

The first Qwen Agent integration targets Windows x64. NVIDIA systems with enough detected VRAM use the pinned CUDA llama.cpp backend; smaller/non-NVIDIA Windows x64 systems use the pinned CPU backend. The CUDA profile keeps llama.cpp memory fitting enabled so it can choose a safe layer split when VRAM is already partly occupied, rather than assuming the entire model must fit at once. CPU inference is substantially slower, but it keeps the optional agent usable without an NVIDIA GPU. Standard language/Standard UI remain broader than this optional IDE feature.
