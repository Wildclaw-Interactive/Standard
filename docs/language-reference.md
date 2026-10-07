# Language Reference

> **Applies to:** Standard `0.1.2-alpha`

Standard is designed so ordinary source reads naturally while still having deterministic syntax and static analysis. The current compiler uses a C#/.NET bootstrap backend, but C# is not part of Standard source code.

## Comments

Use `Note:` for a single-line comment:

```standard
Note: This line is ignored by the program.
health = 100
```

For a multi-line comment, put `Note:` on a line by itself and close the comment with `End`:

```standard
Note:
    This entire block is ignored.
    It can contain punctuation, examples, or disabled code.
    Nothing here is parsed as Standard.
End
```

A `Note:` block that is missing its closing `End` is a compiler error. The same comment forms work in `.standard`, `.standardui`, and `.standardproject` files.

## Assignment and comparison

Standard deliberately keeps assignment and comparison visually different:

```standard
health = 100
Set health to 100

If health is 100:
End
```

Rule of thumb:

> `=` changes a value. `is` asks about a value.

Existing values can also be changed naturally:

```standard
Increase score by 1
Decrease health by 20
```

Compact compound assignment is also supported:

```standard
score += 1
health -= 20
scale *= 2
amount /= 4
remainder %= 3
```

## Inferred values

Declarations remain implicit:

```standard
score = 10
name = "Ada"
alive = true
ratio = 1.5
```

The current alpha can infer `Integer`, `Text`, `Boolean`, and `Decimal` for core expressions. Lists also carry a basic inferred element type where possible.

Explicit type syntax is not required in the current alpha.

## Text and interpolation

Text uses double quotes:

```standard
name = "Ada"
Print "Hello" to console
```

A name can be inserted into text with braces:

```standard
Print "Hello {name}!" to console
```

Common escapes include `\n`, `\r`, `\t`, `\"`, and `\\`.

## Conditions

```standard
If score is at least 10:
    Print "High score" to console
Else if score is above 5:
    Print "Close" to console
Otherwise:
    Print "Keep going" to console
End
```

`Else:` is accepted as the compact equivalent of `Otherwise:`.

Equivalent symbols are allowed:

```standard
If score >= 10 and alive == true:
End
```

## Operators

Natural and symbolic forms normalize to the same core expression operators:

```text
plus / +
minus / -
multiplied by / *
divided by / /
modulo / %
is / ==
is not / !=
is above / >
is below / <
is at least / >=
is at most / <=
and / &&
or / ||
not / !
```

Parentheses can be used when they make grouping clearer:

```standard
result = (2 plus 3) multiplied by 4
```

## Functions

```standard
Function Damage target by amount:
    Return target minus amount
End

health = Damage health by 20
```

Compact conventional calls remain supported when useful:

```standard
sum = Add(10, 20)
```

A function may return without a value:

```standard
Function StopEarly:
    Return
End
```

Natural function calls currently use the compatible bootstrap lowering path; function definitions are represented in the main AST and symbol table.

## Loops

```standard
Repeat 3 times:
    Print "Hello" to console
End

While health is above 0:
    Decrease health by 1
End

For each item in items:
    Print item to console
End
```

Use `Stop loop` to leave the nearest loop and `Continue loop` to skip to its next iteration:

```standard
For each item in items:
    If item is "skip":
        Continue loop
    End

    If item is "done":
        Stop loop
    End

    Print item to console
End
```

`Break` and `Continue` are accepted compact aliases.

## Lists

```standard
names = ["Ada", "Grace"]
Add "Linus" to names
Remove "Ada" from names

For each name in names:
    Print name to console
End

Clear names
```

## Common built-ins

A few frequently used runtime operations are:

```standard
Print "Hello" to console
Wait 1 second
Prompt "Saved!"
accepted = Confirm "Continue?"
Open "https://example.com"

Write "hello" to file "notes.txt"
Append "more" to file "notes.txt"
text = read text from file "notes.txt"
exists = file exists at "notes.txt"
Create folder "Data"
Delete file "old.txt"
```

See the shipped examples for additional file, clipboard, date/time, list, and Standard UI operations.

## Standard UI startup

A UI application's entry source should normally launch its first interface explicitly:

```standard
Show interface "MainWindow.standardui"
```

For convenience, an `Auto` or `Desktop` project with exactly one `.standardui` file can be auto-started if that line is omitted. Projects with multiple interfaces must choose a startup interface explicitly.

## Human diagnostics

The semantic frontend catches simple type contradictions before C# compilation:

```standard
score = 10
score = "ten"
```

produces a Standard-facing error rather than relying on a generated C# compiler message.

Token diagnostics carry line/column information where available, and unterminated strings, blocks, and multi-line `Note:` comments produce Standard-facing diagnostics.

## Current alpha boundaries

The following are intentionally later work rather than syntax to invent today:

- custom objects/types
- modules/imports beyond the current shared project scope
- structured error handling
- stronger optional/null semantics
- generics
- responsive Standard UI Row/Column/Grid layout

Keeping those out of `0.1.2-alpha` avoids locking Standard into rushed syntax just before wider testing.

## Compiler status

The Standard frontend is authoritative for syntax/semantic analysis. Code generation is still being migrated incrementally:

- core expressions: AST → C#
- specialized Standard built-ins: compatible bootstrap lowering
- statement code generation: existing backend while AST emission expands

This split lets the alpha stabilize the language without regressing working Standard UI and built-ins.
