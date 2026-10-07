# Standard

> **Current release:** `0.1.2-alpha`  
> Developed by **Wildclaw Interactive**

Standard is a natural-style compiled programming language designed to make source code easy to read without making the language ambiguous.

`0.1.2-alpha` adds natural multi-line `Note:` comments and tightens the core language/reference before wider alpha testing.

```standard
name = "World"

If name is not "":
    Print "Hello {name}!" to console
End
```

Natural and symbolic forms can coexist:

```standard
area = width multiplied by height
area = width * height

If score is at least 10:
    Print "Qualified" to console
End
```

`=` assigns values. `is` and related natural phrases compare values.

## Downloads

Official binaries are published on this repository's **Releases** page:

- `Standard-Studio-0.1.2-alpha-win-x64.zip` — IDE + toolchain
- `Standard-SDK-0.1.2-alpha-win-x64.zip` — CLI/compiler toolchain without the IDE

See [DOWNLOADS.md](DOWNLOADS.md) and [docs/installation.md](docs/installation.md).

## Quick start

```text
standard new MyApp
cd MyApp
standard run
```

Or open the generated `.standardproject` in Standard Studio.

## Documentation

Start at **[docs/README.md](docs/README.md)**. The documentation filenames are stable and intentionally do not contain release numbers.

## Qwen Agent

Standard Studio includes an optional local **Qwen Agent** that can create and edit complete Standard projects from prompts. The model is not bundled in the Studio ZIP; Standard Studio can download the pinned local Qwen model/runtime on first use. Its coding tools are restricted to `.standard`, `.standardui`, and `.standardproject` files, and its workflow is deliberately bounded to avoid open-ended tool loops.

See [docs/qwen-agent.md](docs/qwen-agent.md).

## Standard UI

Standard includes its own `.standardui` language and visual designer. Avalonia is used underneath as the current cross-platform rendering backend; Standard code does not need to use Avalonia APIs directly.

## Source availability

This public repository intentionally contains **documentation, examples, issue templates, and release information only**. The implementation source code for Standard Studio and the Standard compiler is private and is not part of the public distribution.

## License

Copyright © 2026 **Wildclaw Interactive**. All rights reserved.

You may use Standard for personal or commercial development and sell/distribute applications you create with Standard without paying Standard royalties solely because Standard was used. The Standard IDE/compiler/SDK itself is proprietary and may not be mirrored, rebranded, or redistributed except where `LICENSE.txt` explicitly permits it.

See `LICENSE.txt`, `REDISTRIBUTABLES.txt`, `THIRD_PARTY_NOTICES.md`, and [docs/licensing.md](docs/licensing.md).
