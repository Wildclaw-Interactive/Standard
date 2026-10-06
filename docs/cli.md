# Command Line

> **Applies to:** Standard `0.1.0-alpha`

The Standard SDK includes `standard.exe`. Standard Studio also ships the CLI under its `Toolchain` folder.

## Commands

```text
standard new <name> [folder]
standard init [folder]
standard check [path]
standard build [path]
standard run [path]
standard info [path]
standard version
standard help
```

### `standard new`

Creates a new Standard project, including a `.standardproject` manifest and `Main.standard`.

```text
standard new MyApp
standard new MyApp C:\Projects\MyApp
```

The target folder must be empty when creating a new project.

### `standard init`

Adds a `.standardproject` manifest to an existing folder. If no top-level `.standard` file exists, Standard creates `Main.standard`.

```text
standard init
standard init C:\Projects\ExistingFolder
```

### `standard check`

Runs Standard parsing, semantic analysis, and lowering without invoking the final .NET build.

```text
standard check
standard check MyProject.standardproject
standard check Main.standard
```

### `standard build`

Builds a Standard project or a standalone `.standard` file.

```text
standard build
standard build C:\Projects\MyApp
standard build Hello.standard
```

### `standard run`

Builds and runs a Standard project or standalone `.standard` file.

```text
standard run
standard run Hello.standard
```

### `standard info`

Shows project name, project version, target, entry file, source-file count, and UI-file count.

### `standard version`

Prints the installed Standard toolchain version.

```text
standard version
```

For this release the output is:

```text
0.1.0-alpha
```

## Project discovery

When no path is given, the CLI searches from the current folder upward for a unique `.standardproject` manifest. If none is found, run `standard init` or pass a project/file path explicitly.
