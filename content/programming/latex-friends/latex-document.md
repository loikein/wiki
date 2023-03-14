---
weight: 100
title: "LaTeX Document"
---

# LaTeX Document

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

## Citation in section title

Ref: [tableofcontents - Latex: Citations in section headings put into table of contents first - Stack Overflow](https://stackoverflow.com/a/954224/10668706)

```latex
\section[Section title for running heading]{Section title with citation \cite{key}}
```

## Cross-referencing

### Bookmarks

Section numbers in PDF bookmarks:

```latex
\usepackage[numbered]{bookmark}
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
\documentclass{article}
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

## Remotely related: fuse Markdown with LaTeX

[以 Markdown 撰写文稿，以 LaTeX 排版 | 始终](https://liam.page/2020/03/30/writing-manuscript-in-Markdown-and-typesetting-with-LaTeX/index.html) 

[Markdown 写作，Pandoc 转换：我的纯文本学术写作流程 - 少数派](https://sspai.com/post/64842)
