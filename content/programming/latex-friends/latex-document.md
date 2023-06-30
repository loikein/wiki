---
weight: 100
title: "LaTeX Document"
---

## Debugging (in Shell)

Find out the current version of LaTeX: \([credit](https://superuser.com/a/492743)\)

```bash
pdflatex --version
```

When `\xdef\@fontenc@load@list{\@fontenc@load@list undefined control sequence` happens: \([credit](https://stackoverflow.com/a/60493558/10668706)\)

```bash
fmtutil-sys --all
```

## Pass options to already loaded packages

When `! LaTeX Error: Option clash for package xcolor` \([credit](https://tex.stackexchange.com/a/99051)\)

```latex
\PassOptionsToPackage{dvipsnames}{xcolor}

% before
\documentclass{...}
```

## Compile two versions at one pass

[pdftex - 2 PDF Outputs at once with 2 different styles - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/questions/360192/2-pdf-outputs-at-once-with-2-different-styles)

Or: Arara

## Files control/subfiles

```text
.
├── main.tex
├── slides.tex
├── ref.bib
├── styles
│   ├── aernobold.bst
│   └── aernobold.sty
├── chapters
│   ├── intro.tex
│   ├── sections.tex
│   ├── model.tex
│   └── appendix.tex
└── slides
    ├── intro.tex
    ├── sections.tex
    ├── model.tex
    └── appendix.tex
```

For example, in `main.tex`:

```latex
\bibliographystyle{styles/aernobold}

\begin{document}
  \include{chapters/intro}
  \include{chapters/sections}
  \include{chapters/model}

  \bibliography{ref}

  \appendix
  \include{chapters/appendix}
\end{document}
```

In `chapters/intro.tex` \(first line of file\):

```tex
%!TEX root = ../main.tex
```

### Prevent page breaks around subfiles

**Way 1:** use `\input` \([credit](https://stackoverflow.com/a/1210233/10668706)\)

```latex
\input{file1}
\input{file2}
```

**Way 2:** use `\include` \([credit](https://stackoverflow.com/a/10066885/10668706)\)

{{< hint warning >}}
This method breaks all  cleveref references pointing to labels inside the subfiles. Don't know about normal references.
{{< /hint >}}

```latex
\begingroup
\let\clearpage\relax
\include{file1}
\include{file2}
\endgroup
```

## Citation in section title

Ref: [tableofcontents - Latex: Citations in section headings put into table of contents first - Stack Overflow](https://stackoverflow.com/a/954224/10668706)

```latex
\section[Section title for running heading]{Section title with citation \cite{key}}
```

## Cleveref

```latex
\usepackage{hyperref}
\usepackage[nameinlink]{cleveref}

\begin{document}
\Cref{fig:1} is capitalised, and \cref{fig:1} is not capitalised.
\end{document}
```

## Cross-referencing

### Bookmarks

Section numbers in PDF bookmarks: \(one of them will work depending on your styles\)

```latex
\usepackage[numbered]{bookmark}
\usepackage[bookmarksnumbered]{hyperref}
```

### Equations \& sections

Ref: [Cross-reference packages: which to use, which conflict? - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/a/36312)

TL;DR: use `cleveref`.


### Links

[LaTeX/Labels and Cross-referencing - Wikibooks, open books for an open world](https://en.wikibooks.org/wiki/LaTeX/Labels_and_Cross-referencing)


## Checklists

Ref: [enumerate - How to create checkbox todo list? - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/a/313337)

![](https://i.stack.imgur.com/w1G7s.png)

```latex
\usepackage{enumitem,amssymb}
\newlist{todolist}{itemize}{2}
\setlist[todolist]{label=$\square$}
\usepackage{pifont}
\newcommand{\cmark}{\ding{51}}%
\newcommand{\xmark}{\ding{55}}%
\newcommand{\done}{\rlap{$\square$}{\raisebox{2pt}{\large\hspace{1pt}\cmark}}%
\hspace{-2.5pt}}
\newcommand{\wontfix}{\rlap{$\square$}{\large\hspace{1pt}\xmark}}

\begin{document}
  My ToDo list

  \begin{todolist}
    \item[\done] Frame the problem
    \item Write solution
    \item[\wontfix] profit
  \end{todolist}

\end{document}
```

## Code

### `listings` package

```latex
\usepackage{listings}
\lstset{
  basicstyle=\ttfamily\small,
  breaklines=true
}
\lstMakeShortInline[columns=fixed]|

\begin{document}
  \lstinline|hello, world|

  \begin{lstlisting}[language=Python]
  # help i'm in latex hell
  \end{lstlisting}
\end{document}
```

### `minting` package

> TBE!!

## Page number

### Reset page number at appendix

```latex
\usepackage{appendixnumberbeamer}

\begin{document}
  Words.

  \appendix

  Less important words.
\end{document}
```

## Plots/Images

### Full image

If want to control width:

```latex {hl_lines="3"}
\begin{figure}
  \centering
  \includegraphics[width=\linewidth,keepaspectratio]{figure/great-pic-1.png}
  \caption{A good picture.}
  \label{fig:great-pic-1}
\end{figure}
```

<!-- If want to control height:

```latex {hl_lines="3"}
\begin{figure}
  \centering
  \includegraphics[height=\textheight,keepaspectratio]{figure/great-pic-1.png}
  \caption{A good picture.}
  \label{fig:great-pic-1}
\end{figure}
``` -->

### Vertical subplots

```latex {hl_lines=[5,10]}
\usepackage{subcaption}

\begin{document}
  \begin{figure}
    \begin{subfigure}{\textwidth} 
    \centering
    \includegraphics[width=\linewidth,height=0.8\textheight,keepaspectratio]{images/great-picture-1.png}
    \caption{A good picture.}
    \end{subfigure}
    \begin{subfigure}{\textwidth}
      \centering
      \includegraphics[width=\linewidth,height=0.8\textheight,keepaspectratio]{images/great-picture-2.png}
      \caption{A splendid picture.}
    \end{subfigure}
  \caption{Two great pictures.}
  \end{figure}
\end{document}
```

## Strike through text

```latex
\usepackage[normalem]{ulem}

\begin{document}
  \sout{Bad words.}
\end{document}
```

## Tables

### Make table sideways

```latex {hl_lines=[1,3,10]}
\usepackage{lscape}

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

```latex {hl_lines=[1,5,9]}
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


## Newer and better environment defaults

### List with larger line height

Ref: [How to adjust list spacing | The TeX FAQ](https://texfaq.org/FAQ-complist)

Note: works in Beamer, but does not work with `[<+->]` overlay \(see [Beamer #Bugs & quirks](/programming/latex-friends/beamer/#newenvironment)\)

```latex
\newenvironment{itemize*}%
  {\begin{itemize}%
      \setlength{\parskip}{0.5em}}%
  {\end{itemize}}
```

### More permissible slash and hyphen

Make LaTeX more willing to break line \([Ref](https://tex.stackexchange.com/a/121957)\)

```latex
\makeatletter
\renewcommand{\slash}{/\penalty\z@\hskip\z@skip }
\newcommand{\hyphen}{-\penalty\z@\hskip\z@skip }
\makeatother
```

## Remotely related: fuse Markdown with LaTeX

- [Markdown 写作，Pandoc 转换：我的纯文本学术写作流程 - 少数派](https://sspai.com/post/64842)
