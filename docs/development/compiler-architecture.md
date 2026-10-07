# Compiler Architecture

> **Private development documentation**
>
> Architecture snapshot for Standard `0.1.2-alpha`. This file is for the Wildclaw Interactive development tree and is intentionally not part of the public user documentation set.

## Ordinary Standard

```text
source
  ↓
StandardCommentProcessor
  ↓
StandardLexer
  ↓
StandardSyntaxToken[]
  ↓
StandardParser
  ↓
StandardCompilationUnitSyntax
  ↓
StandardSemanticAnalyzer
  ↓
StandardSemanticModel
  ↓
StandardTranspiler / C# bootstrap backend
  ↓
.NET compiler
```

`StandardFrontend.Analyze(source)` is the single public orchestration point for comment masking, lexing, parsing, and semantic analysis. `StandardCommentProcessor` replaces comment characters with spaces while preserving newlines and source length, so token offsets and diagnostics still point at the original file.

## Syntax layer

Location:

```text
src/Standard.Core/Language/Syntax/
```

The lexer records absolute offsets plus line/column information. The parser creates explicit nodes for core statements and expressions. Specialized commands not yet formally modeled are kept as `StandardCommandSyntax` rather than being discarded.

Natural and symbolic operator spellings normalize to `StandardBinaryOperatorKind` / `StandardUnaryOperatorKind`, so syntax choice does not change semantics.

## Semantic layer

Location:

```text
src/Standard.Core/Language/Semantics/
```

0.1.2-alpha provides:

- function symbols
- project/global variable symbols
- primitive inferred types
- list type groundwork
- numeric compatibility/widening
- incompatible-reassignment diagnostics

The semantic model intentionally uses `Unknown` when a specialized Standard built-in has not yet received a formal expression node. `Unknown` is permissive instead of producing false errors.

## Backend migration

The existing C# backend remains because it already supports the practical Standard surface, Standard UI bridge, desktop helpers, files, console operations, and natural function calls.

0.1.2-alpha begins backend migration with `StandardCSharpExpressionEmitter`: expressions understood by the new AST can emit C# from normalized operator nodes. Specialized expressions fall back to the established lowering rules.

Future releases should move statement groups to AST emission until the old line-oriented lowering is no longer needed.

## Standard UI

Standard UI remains a separate but analogous frontend:

```text
.standardui
  ↓
StandardCommentProcessor
  ↓
StandardUiLexer
  ↓
StandardUiAstParser
  ↓
StandardUiBinder
  ↓
StandardUiDocument
  ↓
Avalonia backend
```

The long-term goal is shared compiler infrastructure where it makes sense without forcing the code language and declarative UI language into one grammar.
