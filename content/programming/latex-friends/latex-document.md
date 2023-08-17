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

## Build & file structures

### Pass options to already loaded packages

When `! LaTeX Error: Option clash for package xcolor` \([credit](https://tex.stackexchange.com/a/99051)\)

```latex
\PassOptionsToPackage{dvipsnames}{xcolor}

% before
\documentclass{...}
```

### Compile two versions at one pass

[pdftex - 2 PDF Outputs at once with 2 different styles - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/questions/360192/2-pdf-outputs-at-once-with-2-different-styles)

Or: Arara (?)

### Files control/subfiles

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

> This method breaks all cleveref references pointing to labels inside the subfiles. Don't know about normal references.
{.book-hint .warning}

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

## Cross-referencing

### Bookmarks

Section numbers in PDF bookmarks: \(one of them will work depending on your styles, `bookmark` is better\)

```latex
\usepackage[bookmarksnumbered]{hyperref}

\usepackage[numbered]{bookmark}
```

Manually add bookmarks: \([ref](https://tex.stackexchange.com/a/35430)\)

```latex
% if using numbered bookmarks
\usepackage[numbered]{bookmark}
\bookmarksetup{startatroot}
\currentpdfbookmark{Bibliography}{bibliography}
\bibliography{ref}

% note: don't use, will mess with appendix bookmark levels:
% \bookmark[level=0,named=Bibliography]{Bibliography}

% if using unnumbered bookmarks
\pdfbookmark[section]{Bibliography}{bibliography}
\bibliography{ref}
```

### Equations \& sections

Ref: [Cross-reference packages: which to use, which conflict? - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/a/36312)

TL;DR: use `cleveref`.


### Links

[LaTeX/Labels and Cross-referencing - Wikibooks, open books for an open world](https://en.wikibooks.org/wiki/LaTeX/Labels_and_Cross-referencing)


## Checklists

Ref: [enumerate - How to create checkbox todo list? - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/a/313337)

{{< figure
src="https://i.stack.imgur.com/w1G7s.png"
w="300px"
alt="LaTeX checklist"
>}}

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

## Code display

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


## Formatting text

### Highlight

```latex
\usepackage{soul}

% can be used with various colours
\usepackage[dvipsnames]{xcolor}
\sethlcolor{GreenYellow}
% or even custom colours (also with xcolor)
\definecolor{highlight}{HTML}{FFFF81}
\sethlcolor{highlight}

\begin{document}
  \hl{Good words.}
\end{document}
```

### Strike through

With package soul:

```latex
\usepackage{soul}

\begin{document}
  \st{overstriking}
\end{document}
```

With package ulem:

```latex
\usepackage[normalem]{ulem}

\begin{document}
  \sout{Bad words.}
\end{document}
```


## Maths

### Too much space around display math

Ref: [line spacing - Spaces around display math when using setspace - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/a/55488)

```latex
\usepackage[nodisplayskipstretch]{setspace}

\begin{document}
…
\end{document}
```


## Page number

### Reset page number at appendix

Ref: [Restart page numbering for memoir appendix - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/a/259106)

```latex
\begin{document}
% Words.

  \clearpage
  \pagenumbering{arabic}
% \setcounter{page}{0}
  \appendix

% Less important words.
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

## Packages

### Cleveref

```latex
\usepackage{hyperref}
\usepackage[nameinlink]{cleveref}

\begin{document}
\Cref{fig:1} is capitalised, and \cref{fig:1} is not capitalised.
\end{document}
```

### siunitx

Thousands separator:

```latex
\usepackage{siunitx}
\sisetup{
  group-separator = {,},
  group-minimum-digits = 4,
}

\begin{document}
\SI{15663}{}    % The empty braces are necessary for correct spacing
                % Gives: 15,663
\end{document}
```


## Remotely related: fuse Markdown with LaTeX

- [Markdown 写作，Pandoc 转换：我的纯文本学术写作流程 - 少数派](https://sspai.com/post/64842)
