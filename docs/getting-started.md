# Getting Started

> **Applies to:** Standard `0.1.2-alpha`

This guide creates a small multi-file-capable Standard project using the CLI. The same project can also be opened in Standard Studio.

## 1. Create a project

```text
standard new MyApp
cd MyApp
```

This creates a `.standardproject` manifest and an entry `.standard` source file.

## 2. Write Standard code

Open `Main.standard` and try:

```standard
name = "World"

If name is not "":
    Print "Hello {name}!" to console
End
```

Standard keeps assignment and comparison intentionally distinct:

```standard
health = 100

If health is at least 50:
    Print "Ready" to console
End
```

- `=` changes a value.
- `is`, `is not`, `is above`, `is below`, `is at least`, and `is at most` compare values.
- Natural and symbolic math forms may be mixed where supported.

## 3. Check the project

```text
standard check
```

This runs Standard parsing and semantic analysis without performing the final .NET build.

## 4. Run it

```text
standard run
```

## 5. Add more files

Add more `.standard` files anywhere under the project folder. In the current alpha, project source files share one project scope, so helper functions can live in separate files without import boilerplate.

## 6. Build a UI

Create a `.standardui` file in Standard Studio to use the visual designer, or write the UI format directly. See [Standard UI](standard-ui.md).

## Where to go next

- [Language Reference](language-reference.md)
- [Projects](projects.md)
- [Command Line](cli.md)
- [Standard UI](standard-ui.md)
