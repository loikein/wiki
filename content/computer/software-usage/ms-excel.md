---
weight: 400
title: "Microsoft Excel"
---

[Syntax highlighting for Excel Formulae - language suggestions - Meta Stack Exchange](https://meta.stackexchange.com/questions/362351/syntax-highlighting-for-excel-formulae-language-suggestions) (Using `scala` here.)

## Reference

- Cell: `A1`, `B3`, `A1:B3`
- Column: `B:B`
- Row: `3:3`
- Sheet: `'Sheet 1'!B3:B40`
- Keep reference position when batch applying: `$A$1:$B$3`

{{< hint warning >}}
Single and double quotations are strictly different. Single quotation is only used when:

- Referencing to sheet names
- Put in the beginning of number cell to make it a string cell
{{< /hint >}}

## Functions

### `CONCAT`

[CONCAT function - Microsoft Support](https://support.microsoft.com/en-us/office/concat-function-9b1a9a3f-94ff-41af-9736-694cbd6b4ca2)

Stitch strings \& values of cells together.

```scala
CONCAT("Words", A1, B3, ...)
```

### `COUNTIF`, `COUNTIFS`

[COUNTIF function - Microsoft Support](https://support.microsoft.com/en-au/office/countif-function-e0de10c6-f885-4e71-abb4-1f464816df34)  
[COUNTIFS function - Microsoft Support](https://support.microsoft.com/en-us/office/countifs-function-dda3dc6e-f74e-4aee-88bc-aa8c2a866842)

Count rows that meet conditions.

OR:

```scala
COUNTIF(<cells>, <condition>) + COUNTIF(...) + ...
```

AND:

```scala
COUNTIFS(
    <cells>,        // B2:B62
    <condition>     // ">0"
    // can be repeated multiple times
)
```

### `IFERROR`

[IFERROR function - Microsoft Support](https://support.microsoft.com/en-us/office/iferror-function-c526fd07-caeb-47b8-8bb6-63f3e417f611)

Set default value for when function returns an error.

```scala
IFERROR(
    <function>,
    <default value> // ""
)
```

### `ROUND`, `ROUNDUP`, `ROUNDDOWN`

[ROUND function - Microsoft Support](https://support.microsoft.com/en-au/office/round-function-c018c5d8-40fb-4053-90b1-b3e7f61a213c)  
[ROUNDUP function - Microsoft Support](https://support.microsoft.com/en-us/office/roundup-function-f8bc9b23-e795-47db-8703-db171d0c42a7)  
[ROUNDDOWN function - Microsoft Support](https://support.microsoft.com/en-us/office/rounddown-function-2ec94c73-241f-4b01-8c6f-17e6d7968f53)

```scala
ROUND / ROUNDUP / ROUNDDOWN(
    <cell>,     // B2
    <decimals>  // 0
)
```

### `VLOOKUP`

[VLOOKUP function - Microsoft Support](https://support.microsoft.com/en-us/office/vlookup-function-0bbc8083-26fe-4963-8ab8-93a18ad188a1)

Look up code and return values from an area of codebook.

```scala
VLOOKUP(
    <cell of code>,                 // B3
    <cells of codebook>,            // $R$3:$T$20
    <column to return in codebook>, // (1-base)
    <Approximate (1) or Exact (0)>  // 0
)
```
