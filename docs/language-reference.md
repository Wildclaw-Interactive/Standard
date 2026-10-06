# Language Reference

> **Applies to:** Standard `0.1.0-alpha`

Standard source is analyzed by the language frontend before the current C#/.NET bootstrap backend performs final code generation and compilation.

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

Equivalent symbols are allowed:

```standard
If score >= 10 and alive == true:
End
```

## Math

Both forms are valid:

```standard
area = width multiplied by height
area = width * height
```

The AST normalizes both to the same `Multiply` operator kind.

Supported core pairs:

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

## Lists

```standard
names = ["Ada", "Grace"]
Add "Linus" to names

For each name in names:
    Print name to console
End
```

## Human diagnostics

The semantic frontend catches simple type contradictions before C# compilation:

```standard
score = 10
score = "ten"
```

produces a Standard-facing error rather than relying on a generated C# compiler message.

Token diagnostics now also carry column/length information where available, establishing the source-range foundation for richer IDE squiggles later.

## Compiler status

The Standard frontend is authoritative for syntax/semantic analysis. Code generation is in migration:

- core expressions: AST → C#
- specialized Standard built-ins: compatible bootstrap lowering
- statement code generation: existing backend while AST emission is expanded

This split is intentional so the alpha can stabilize the compiler foundation without regressing working Standard UI and built-ins.
