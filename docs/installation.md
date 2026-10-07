# Installation

> **Applies to:** Standard `0.1.2-alpha`

Standard is distributed by **Wildclaw Interactive** as proprietary binary software. The Standard compiler and Standard Studio implementation source are not included in public releases.

## Choose a package

### Standard Studio

Download:

```text
Standard-Studio-0.1.2-alpha-win-x64.zip
```

This package includes the Standard Studio IDE and the Standard command-line toolchain. Extract it to a normal writable folder and run `Standard.Studio.exe`.

### Standard SDK

Download:

```text
Standard-SDK-0.1.2-alpha-win-x64.zip
```

Use this package if you want the Standard compiler/CLI without Standard Studio. Run `standard.exe` from the extracted folder or add that folder to your `PATH`.

## Current .NET requirement

Standard currently uses C#/.NET as its bootstrap backend for the final application build. A compatible **.NET 8 SDK** must therefore be installed on machines that compile Standard applications.

Finished applications do not need Standard Studio or the Standard SDK merely to run; they use whatever runtime/dependencies were produced by their own build or publish process.

## Optional Qwen Agent

The Qwen Agent is included in Standard Studio itself, but the model and local inference runtime are **not** bundled in the Studio ZIP. On first use, choose **Install Qwen AI** and approve the download. The initial download is roughly 6 GB.

The first Qwen Agent release targets Windows x64. NVIDIA systems use the pinned CUDA backend when suitable; other Windows x64 systems use a CPU fallback. After installation, Studio does not load the multi-gigabyte model into RAM/VRAM until you click **Load Qwen AI**.

See [Qwen Agent](qwen-agent.md) for workflow, privacy, backups, and validation details.

## Verify the installation

```text
standard version
standard help
```

`standard version` should report `0.1.2-alpha`.

## Next step

Continue with [Getting Started](getting-started.md).

## License

Using Standard to create personal or commercial software is permitted under `LICENSE.txt`. Redistribution of the Standard Studio/compiler/SDK itself is restricted. See [Licensing and Distribution](licensing.md) and the root `REDISTRIBUTABLES.txt`.
