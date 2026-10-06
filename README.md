# Standard

> **Current release:** `0.1.0-alpha`  
> Developed by **Wildclaw Interactive**

Standard is a natural-style compiled programming language designed to make source code easy to read without making the language ambiguous.

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

- `Standard-Studio-0.1.0-alpha-win-x64.zip` — IDE + toolchain
- `Standard-SDK-0.1.0-alpha-win-x64.zip` — CLI/compiler toolchain without the IDE

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

## Standard UI

Standard includes its own `.standardui` language and visual designer. Avalonia is used underneath as the current cross-platform rendering backend; Standard code does not need to use Avalonia APIs directly.

## Source availability

This public repository intentionally contains **documentation, examples, issue templates, and release information only**. The implementation source code for Standard Studio and the Standard compiler is private and is not part of the public distribution.

## License

Copyright © 2026 **Wildclaw Interactive**. All rights reserved.

You may use Standard for personal or commercial development and sell/distribute applications you create with Standard without paying Standard royalties solely because Standard was used. The Standard IDE/compiler/SDK itself is proprietary and may not be mirrored, rebranded, or redistributed except where `LICENSE.txt` explicitly permits it.

See `LICENSE.txt`, `REDISTRIBUTABLES.txt`, `THIRD_PARTY_NOTICES.md`, and [docs/licensing.md](docs/licensing.md).
