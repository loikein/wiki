---
weight: 100
title: "Tables"
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
\usepackage{makecell}

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

### Combining everything

Usage of `\multirowcell`:  
`\multirowcell{<nrow>}[<vmove>][<hor alignment>]{<contents>}` \([CTAN: Package makecell](https://ctan.org/pkg/makecell?lang=en)\)

Using `\multirowcell{<nrow>}[0pt][<alignment>]` here.

{{< figure
name="latex_table_all.png"
w="400px"
alt="LaTeX table with a multi-row-multi-cell linebreaking cell"
>}}

```latex
\usepackage{makecell}

\begin{table}\centering
  \caption{Good table with everything}\label{tab:all}
  \begin{tabular}{lll}
    {} \\[-1.8ex]\hline
    \hline \\[-1.8ex]
    Head Col 1 &  \multicolumn{2}{c}{\multirowcell{2}[0pt][l]{Not head col\\ any more}}
    \cr \cline{1-1} \\[-1.8ex]
    Data Col 1 &  \\ \hline \\[-1.8ex]
    Data Col 1 & Data Col 2 & Data Col 3 \\ \hline \\[-1.8ex]
    Data Col 1 & Data Col 2 & Data Col 3 \\
    \hline
    \hline \\[-1.8ex]
  \end{tabular}
\end{table}
```


## Table

### Add end notes

Stargaze does this automatically, but I was not happy that a particularly long note would widen the table. [A comment in this question](https://tex.stackexchange.com/questions/12676/add-notes-under-the-table#comment22909_12676) solved that problem for me.

> If you have used `\begin{tabular}{@{\extracolsep{5pt}}lcc}`, write `\multicolumn{3}{p{\textwidth}}{\hspace{-6pt}\textit{Notes:} ...}` instead. The pixels for `\hspace` should be adjusted on a case-by-case basis.
> 
> This is because `\multicolumn` does not take the whole `\linewidth`, as explained [here](https://tex.stackexchange.com/a/532894/206709).
{.book-hint .info}

```latex {hl_lines="12"}
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
    \multicolumn{3}{p{\textwidth}}{\textit{Notes:} $^{\ast}p<0.1$; $^{\ast\ast}p<0.05$; $^{\ast\ast\ast}p<0.01$.}
  \end{tabular}
\end{table}
```

### Make table sideways

Ref: [rotating - Vertical orientation landscape page in a PDF output file - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/a/231507)

```latex {hl_lines="5 12"}
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

```latex {hl_lines="5 9"}
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
