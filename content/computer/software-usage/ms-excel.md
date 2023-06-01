---
weight: 400
title: "Microsoft Excel"
---

# Microsoft Excel

[Syntax highlighting for Excel Formulae - language suggestions - Meta Stack Exchange](https://meta.stackexchange.com/questions/362351/syntax-highlighting-for-excel-formulae-language-suggestions) (Using `scala` here.)

## Reference

- Cell: `A1`, `B3`
- Column: `B:B`
- Row: `3:3`
- Sheet: `'Sheet 1'!B3`


## Functions

### `CONCAT`

Stitch strings \& values of cells together.

```scala
CONCAT("Words", A1, B3, ...)
```

### `IFERROR`

```scala
IFERROR(
    <function>,
    <default value if got error>   // ""
)
```

### `VLOOKUP`

```scala
VLOOKUP(
    <cell of code>,                 // B3
    <cells of codebook>,            // $R$3:$T$20
    <column to return in codebook>, // (1-base)
    <Approximate (1) or Exact (0)>  // 0
)
```
