---
weight: 100
title: "LaTeX Tables"
---

## Cell


### Line breaks inside cell

Refs:

- [Table with multiple lines in some cells - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/a/501507)
- [tables - How to vertically AND left-align a cell with \\makecell? - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/a/410686)

The `\hline`'s are a hack without using any extra packages.

{{< figure
name="latex_table_makecell.png"
w="400px"
alt="LaTeX table with line breaks in cells"
>}}

```latex {hl_lines="8-10"}
\begin{table}\centering
  \caption{Good table with line breaks}\label{tab:line-break}
  
  \begin{tabular}{lll}
    {} \\[-1.8ex]\hline
    \hline \\[-1.8ex]
    Head Col 1 & Head Col 2 & Head Col 3 \\ \hline \\[-1.8ex]
    Data Col 1 & Data Col 2 & \makecell[l]{here is \\ my text \\ centre-aligned} \\ \hline \\[-1.8ex]
    Data Col 1 & Data Col 2 & \makecell[tl]{here is \\ my text \\ top-aligned} \\ \hline \\[-1.8ex]
    Data Col 1 & Data Col 2 & \makecell[br]{here is \\ my text \\ bottom-aligned} \\
    \hline
    \hline \\[-1.8ex]
  \end{tabular}
\end{table}
```

### Multi-column cell

Replace any x cells with the code below, and continue as if you have put x cells.

```latex
\multicolumn{x}{l|r|c}{Cell contents…}
```

### Multi-row cell

Ref: [tables - How to use \\multirow correctly? - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/a/585927)

{{< figure
name="latex_table_multirow.png"
w="400px"
alt="LaTeX table with a multi-row cell"
>}}

```latex {hl_lines="8"}
\usepackage{multirow}

\begin{table}\centering
  \caption{Good table with multiple row cells}\label{tab:multi-row}
  \begin{tabular}{lll}
    {} \\[-1.8ex]\hline
    \hline \\[-1.8ex]
    \multirow{4}{*}{Head Col 1} & Head Col 2 & Head Col 3 \\
     & Data Col 2 & Data Col 3 \\
     & Data Col 2 & Data Col 3 \\
     & Data Col 2 & Data Col 3 \\
    \hline
    \hline \\[-1.8ex]
  \end{tabular}
\end{table}
```


## Table

### Make table sideways

Ref: [rotating - Vertical orientation landscape page in a PDF output file - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/a/231507)

```latex {hl_lines=[5,12]}
% choose one of the two packages:
\usepackage{lscape}     % if want the page upright
\usepackage{pdflscape}  % if want the page sideways

\begin{landscape}
\begin{table} \centering
\caption{Great table}\label{tab:great-table}
\begin{tabular}
...
\end{tabular}
\end{table}
\end{landscape}
```

### Shrink tables that are too big

Ref: [scaling - Is there a way to slightly shrink a table, including font size, to fit within the column boundaries? - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/a/10865)

My setup somehow does not like `adjustbox` or `\resizebox`. Will update if tested.

```latex {hl_lines=[5,9]}
\usepackage{graphicx}

\begin{table} \centering
\caption{Great table}\label{tab:great-table}
\scalebox{0.85}{%
\begin{tabular}
...
\end{tabular}
}% end scalebox
\end{table}
```
