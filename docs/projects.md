# Projects

> **Applies to:** Standard `0.1.2-alpha`

A Standard project is a normal folder containing exactly one `.standardproject` manifest at its root.

```standard
Project "Tic Tac Toe":
    Version "0.1.0"
    Entry "MainWindow.standard"
    Target Desktop
End
```

> `Version` in a `.standardproject` file belongs to **your application**, not to the installed Standard toolchain. New projects currently begin at `0.1.0`.

## Project settings

- `Project "Name":` — the project display name.
- `Version "..."` — your application's version string.
- `Entry "file.standard"` — the source file containing project startup code.
- `Target Auto|Console|Desktop` — the project target.
- `End` — closes the project manifest.

## Multi-file projects

Every `.standard` file under the project root is included recursively except files inside generated/development folders such as `bin`, `obj`, `.git`, and `.standard`.

```text
MyGame/
├── MyGame.standardproject
├── Main.standard
├── Game.standard
├── Player.standard
└── UI/
    ├── MainWindow.standard
    └── MainWindow.standardui
```

The current alpha intentionally uses one shared project scope. That means helper functions can live in separate `.standard` files without import boilerplate. Formal modules/namespaces are planned for later without making small projects unnecessarily verbose.

## Entry file

The `Entry` file is the startup source for the project. The current bootstrap backend composes helper source before the entry source so project-visible helpers are available when startup code executes.

For UI projects, put the startup interface in the entry source:

```standard
Show interface "MainWindow.standardui"
```

As a convenience, an `Auto` or `Desktop` project with exactly one `.standardui` file will auto-start that interface if the startup line is missing. This makes a newly created/simple UI project runnable by default. Projects with multiple UI files must explicitly choose the startup interface.

## CLI project discovery

From inside a project folder:

```text
standard check
standard build
standard run
standard info
```

You can also pass a project folder or `.standardproject` path explicitly. See [Command Line](cli.md).

## Standard Studio

Standard Studio discovers the `.standardproject` manifest when you open the project folder. Build and Run operate on the project, not merely on whichever editor tab is active.

The project hierarchy can create `.standard` files, `.standardui` files, and folders.

## Current alpha limitation

Some diagnostics from multi-file builds can still refer to composed-source line positions rather than the perfect original file/range. The lexer already records token source ranges; preserving file identity through every compilation stage is ongoing stabilization work.


## Comments

Project manifests use the same Standard comment style as source files:

```standard
Note: one-line project note

Note:
    Multi-line project documentation.
End
```

Settings written inside a `Note:` block are ignored.
