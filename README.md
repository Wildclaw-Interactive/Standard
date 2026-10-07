# Standard

> **Public release:** `0.1.2-alpha`  
> **Owner:** Wildclaw Interactive  
> **This repository tree is private development source and must not be published.**

Standard is a natural-style compiled programming language designed to keep source code easy to read while retaining deterministic grammar, static analysis, and practical performance.

`0.1.2-alpha` adds natural multi-line `Note:` comments and tightens the core language/reference before wider alpha testing.

```standard
name = "World"

If name is not "":
    Print "Hello {name}!" to console
End
```

## Build the private development tree

```text
dotnet build Standard.sln
dotnet run --project tests/Standard.Core.Tests/Standard.Core.Tests.csproj
```

## Create public distributions

```text
packaging\publish-distribution.cmd
```

The packaging script creates stripped Standard Studio and Standard SDK binaries plus a source-free public GitHub repository payload under `dist/`.

See [packaging/README.md](packaging/README.md) and [docs/licensing.md](docs/licensing.md).

## Local Qwen Agent

Standard Studio `0.1.2-alpha` includes the optional local Qwen Agent introduced in `0.1.1-alpha`. On first use, Studio can download the pinned Qwen model and llama.cpp runtime automatically. The agent only edits Standard project files and uses a bounded Planner → Worker → Quick Tests → Build → Evaluator workflow.

See [docs/qwen-agent.md](docs/qwen-agent.md).

## Documentation

User-facing documentation starts at [docs/README.md](docs/README.md).

Private developer documentation lives under `docs/development/`.

The release history is maintained in [CHANGELOG.md](CHANGELOG.md), while future work is tracked in [ROADMAP.md](ROADMAP.md).

## License

Copyright © 2026 **Wildclaw Interactive**. All rights reserved.

Standard Studio, the Standard compiler, CLI, and SDK are proprietary binary software. Users may use Standard for personal or commercial projects and distribute/sell applications created with Standard without Standard royalties. Redistribution or rebranding of the Standard toolchain itself is restricted by `LICENSE.txt`.

The public GitHub repository intentionally does **not** contain this private implementation source.
