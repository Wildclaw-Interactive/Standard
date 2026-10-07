# Changelog

## 0.1.2-alpha

Language-completeness and documentation pass.

Highlights:

- added natural multi-line comments with `Note:` ... `End`
- multi-line comments work consistently in `.standard`, `.standardui`, and `.standardproject` files
- unterminated `Note:` blocks now produce a clear Standard-facing diagnostic
- Standard Studio syntax coloring and completion now understand multi-line comments
- Qwen's always-on Standard cheat sheet now includes comment syntax, loop control, and compact compound assignment
- language reference expanded for comments, interpolation, compound assignment, `Else`, loop control, lists, common built-ins, and UI startup
- documented existing `Stop loop` / `Continue loop` (`Break` / `Continue`) support
- kept larger syntax additions such as objects, structured error handling, modules, and responsive UI layout out of this stabilization release

## 0.1.1-alpha

### UI startup reliability hotfix

- Fixed simple Standard UI projects building successfully and then exiting immediately when the entry backend forgot `Show interface`.
- `Auto`/`Desktop` projects with exactly one `.standardui` file now auto-start that interface when startup is otherwise unambiguous.
- Running a loose `.standardui` file (or its paired backend) now gets the same build-time startup safety net.
- On Windows, generated Standard UI apps now launch their WinExe apphost directly instead of invoking `dotnet <app>.dll`, avoiding the unnecessary console flash.
- Qwen's permanent cheat sheet now explicitly requires runnable UI entry code, and quick checks reject ambiguous multi-UI projects with no startup interface.

### Qwen worker protocol hotfix

- Simplified `write_file` to a raw `CONTENT:` protocol with no JSON escaping or Markdown fence requirement.
- Made the worker parser tolerate raw content, fenced content, and legacy JSON actions.
- Fixed cases where a valid write path was accepted while the file body was silently lost, causing repeated `write_file requires content` failures.


Standard Studio Qwen Agent update.

Highlights:

- optional local Qwen3.5 9B agent integrated into Standard Studio
- first-use managed model + pinned llama.cpp/CUDA download with resume and SHA256 verification
- Qwen panel appears only after the local model is loaded and ready
- project-aware Planner → Worker → Quick Tests → Build → Evaluator workflow
- hard model-turn and repair limits to prevent open-ended agent loops
- Standard-only file tools restricted to `.standard`, `.standardui`, and `.standardproject`
- automatic per-task backups under `.standard/agent-backups/`
- always-in-context Standard language/UI cheat sheet
- deterministic Standard parser/UI checks and real build validation
- hotfix: corrected Qwen agent raw-string prompt literals and UI backend confirmation dialog compilation
- hotfix: fixed the Qwen downloader hashing its own still-open `.part` file; completed/interrupted downloads are now recovered and verified before any re-download, with transient sharing-violation retries

## 0.1.0-alpha

Initial public alpha by Wildclaw Interactive.

Highlights:

- natural and symbolic Standard syntax
- real lexer/parser/AST with early semantic/type analysis
- multi-file `.standardproject` projects
- Standard CLI
- Standard Studio IDE with syntax coloring and basic completion
- Standard UI designer and `.standardui` format
- Avalonia-backed generated desktop UI
- source-free proprietary binary distribution model
