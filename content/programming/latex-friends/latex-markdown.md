---
weight: 500
title: "Markdown in LaTeX"
---

> After the experiments below, I have decided that this package is not yet fully production-ready, and am now only using it for snippets (e.g. lists). May come back and re-evaluate in the future.
{.book-hint .warning}

- [CTAN: Package markdown](https://ctan.org/pkg/markdown)
- Repo: [Witiko/markdown: :notebook_with_decorative_cover: A package for converting and rendering markdown documents in TeX](https://github.com/Witiko/markdown)
- Doc: [Markdown Package User Manual](https://witiko.github.io/markdown/)


## Compile

```sh
lualatex -synctex=1 -interaction=nonstopmode
```

## Quick start template

> `tightLists=false` is necessary immediately at `\usepackage` to prevent clashing with `enumitem` package. See [Witiko/markdown Issue #84](https://github.com/Witiko/markdown/issues/84#issuecomment-872450573) for more details.
> 
> Also, cannot use `fancyLists` because it also loads the `paralist` package per [Witiko/markdown Pull Request #241](https://github.com/Witiko/markdown/pull/241).
{.book-hint .info}

```latex
\documentclass{article}

\usepackage[tightLists=false]{markdown}
\markdownSetup{
  footnotes = true,
  inlineFootnotes = true,
  renderers = {
    link = {\href{#3}{#1}},
  },
}

\title{Weekly Report}
\author{loikein}

\begin{document}
\maketitle
\begin{markdown}
# Section title

Things ^[Footnotes], [links](#) [^2][^3]

[^2]: More footnotes.

[^3]: Must have line breaks in-between footnotes.
\end{markdown}
\end{document}
```

## Bookmarks with section numbers

Ref: [hyperref - How to put number of chapter and section in the bookmarks of the .pdf - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/a/470748)

```latex
% by default markdown introduces hyperref
\PassOptionsToPackage{bookmarksnumbered}{hyperref}
\documentclass{article}
```

## Hyperlinks

### Render inline hyperlinks

Ref: [以 Markdown 撰写文稿，以 LaTeX 排版 | 始终](https://liam.page/2020/03/30/writing-manuscript-in-Markdown-and-typesetting-with-LaTeX/index.html#%E8%B6%85%E9%93%BE%E6%8E%A5%E5%92%8C%E8%84%9A%E6%B3%A8)

> For more details, see [Witiko/markdown Discussion #273](https://github.com/Witiko/markdown/discussions/273).
> 
> Caution: this setup will bug all relative references within the Markdown environment. I have had no success with the `\renewcommand` solution the author suggested, even with `\makeatletter`.
{.book-hint .warning}

```latex
\usepackage{markdown}
\markdownSetup{
  renderers = {
    link = {\href{#3}{#1}},
  }
}
```


## Images

Ref: [以 Markdown 撰写文稿，以 LaTeX 排版 | 始终](https://liam.page/2020/03/30/writing-manuscript-in-Markdown-and-typesetting-with-LaTeX/index.html#%E6%9B%B4%E5%A5%BD%E5%9C%B0%E6%8F%92%E5%85%A5%E5%9B%BE%E7%89%87)

```latex
\usepackage{graphicx}
\usepackage{markdown}
\markdownSetup{
  relativeReferences = true,
  renderers = {
    image = {\begin{figure}
        \centering
        \includegraphics[width = .8\linewidth]{#3}%
        \ifx\empty#4\empty\else
        \caption{#4}\label{fig:#1}%
        \fi
    \end{figure}},
  },
}

\begin{document}
\begin{markdown}
![fig-1](../plot/fig1.png 'Title of a great pic')

See <fig:fig-1>.
\end{markdown}
\end{document}
```

## Lists

Must have 4 spaces between levels \(don't know about tabs\):

```latex
\begin{document}
\begin{markdown}
- First level
    - Second level
\end{markdown}
\end{document}
```

Can use all `1.` for ordered lists:

```latex
\begin{document}
\begin{markdown}
1. First item
1. Second item
1. Third item
\end{markdown}
\end{document}
```

## Maths

```latex
\usepackage{markdown}
\markdownSetup{
  hybrid = true,
}

\begin{document}
\begin{markdown}
Inline $x=y$ maths. Note: \& must be escaped.

Numbered display equation. Note: `equation*` does not work.

\begin{equation}
  I = \int^a_b x^2 dx
\end{equation}
\end{markdown}
\end{document}
```
