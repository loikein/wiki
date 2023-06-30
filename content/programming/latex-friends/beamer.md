---
weight: 400
title: "Beamer"
---

## Bugs \& quirks

### `\newenvironment<>`

Does not make environment incremental-overlay-aware, aka, cannot use `[<+->]`.

### `<0>` frames

`\begin{frame}<0>`
:   Hides a frame in presentation (default) mode (not handout mode), and does not count the frame in total pages

`\begin{frame}<mode/all:0>`
:   Hides a frame in given mode/all modes, but counts the frame in total pages.

### Natbib colouring problem

This solution only colours the closing bracket, but the link scope stays the same (without closing bracket). (Ref: [1](https://tex.stackexchange.com/questions/369710/beamer-citation-coloring), [2](https://tex.stackexchange.com/a/165015), [seems to be fixed](https://github.com/josephwright/beamer/issues/114) but not really)

```latex
\let\oldcite=\cite
\renewcommand{\cite}[1]{\textcolor{NordGreen}{\oldcite{#1}}}
```

### `! Illegal parameter number in definition of \iterate.`

Ref:  [tikz pgf - Error: Illegal Parameter number in definition of \iterate - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/a/420454)

Whenever there is `#` in a Beamer frame, must write `\#` (tested, URL will work) or `####` (not tested), or mark the frame as fragile (`\begin{frame}[fragile]`).

## Buttons

Ref: [A Tutorial for Beginners (Part 3)—Blocks, Code, Hyperlinks and Buttons - Overleaf, Online LaTeX Editor](https://www.overleaf.com/learn/latex/Beamer_Presentations%3A_A_Tutorial_for_Beginners_(Part_3)%E2%80%94Blocks%2C_Code%2C_Hyperlinks_and_Buttons)

```latex
\begin{frame}
  \frametitle{Summary}\label{summary}
  \hyperlink{details}{\beamergotobutton{Details}}
\end{frame}

\begin{frame}
  \frametitle{Details}\label{details}
  \hyperlink{summary}{\beamerreturnbutton{Return}}
\end{frame}
```

## Note page

### Show note pages

Ref: [1](https://brandonrozek.com/blog/notes-beamer-latex/), [2](https://gist.github.com/andrejbauer/ac361549ac2186be0cdb)

```latex
%\setbeameroption{hide notes} % Only slides
%\setbeameroption{show only notes} % Only notes
\setbeameroption{show notes on second screen=right} % Both
```

### Write notes

Inside frames: (default outcome: 1 `enumerate` list per frame)

```latex
\begin{frame}
  \frametitle{Blah}
  \note[item]{Notes...}
  \note[item]{...blah.}
\end{frame}
```

Outside frames: (default outcome: 1 `itemize` list per frame)

```latex
\begin{frame}
  \frametitle{Blah blah}
\end{frame}

\note[itemize]{
  \item Notes...
  \item ...blah blah.
}
```

### Overlay-aware notes

In incremental overlay:

```latex
\begin{frame}
  \frametitle{Blah}

  \begin{itemize}[<+->]
    \item<.-> 1st slide \& stay
    \note[item]<.>{1st slide only}
    \note[item]<+>{2nd slide only}
    \item 3rd slide \& stay
    ...
  \end{itemize}

\end{frame}
```

### Plain template but change line height

In Intel Macs, Beamer internal styles are stored at path `/usr/local/texlive/2022/texmf-dist/tex/latex/beamer/`. Commands used in note page are stored in  file `beamerbasenotes.sty`, and templates for note page are stored in file `beamerbaseauxtemplates.sty`.

After close inspections, I found these lines to be relevant: \([Ref](https://tex.stackexchange.com/a/28967)\)

```latex {hl_lines=[5,8,18]}
\makeatletter
% For outside frame notes, beamerbasenotes.sty L64-69
% First three lines seems redundant because outside notes always use itemize
\define@key{beamernotes}{enumerate}[true]{%
  \def\beamer@noteenvstart{\begin{enumerate}\itemsep=0pt\parskip=8pt}%
    \def\beamer@noteenvend{\end{enumerate}}}
\define@key{beamernotes}{itemize}[true]{%
  \def\beamer@noteenvstart{\begin{itemize}\itemsep=0pt\parskip=8pt}%
    \def\beamer@noteenvend{\end{itemize}}}

% For inside frame notes, beamerbasenotes.sty L178-195
\def\beamer@setupnote{%
  \gdef\beamer@notesactions{%
    \beamer@outsideframenote{%
      \beamer@atbeginnote%
      \beamer@notes%
      \ifx\beamer@noteitems\@empty\else
      \begin{enumerate}\itemsep=0pt\parskip=8pt%
        \beamer@noteitems%
      \end{enumerate}%
      \fi%
      \beamer@atendnote%
    }%
    \gdef\beamer@notesactions{}%
  }
}
\makeatother
````

Changing the values of `\itemsep` and `\parskip` in all three instances will give different line height results.

### Use `itemize` for both inside and outside slides

Just change the inside notes above from `enumerate` to `itemize`. \([Ref](https://tex.stackexchange.com/a/28967)\)

```latex {hl_lines=[8,10]}
\makeatletter
\def\beamer@setupnote{%
  \gdef\beamer@notesactions{%
    \beamer@outsideframenote{%
      \beamer@atbeginnote%
      \beamer@notes%
      \ifx\beamer@noteitems\@empty\else
      \begin{itemize}\itemsep=0pt\parskip=8pt%
        \beamer@noteitems%
      \end{itemize}%
      \fi%
      \beamer@atendnote%
    }%
    \gdef\beamer@notesactions{}%
  }
}
\makeatother
```

### Insert vertical space above notes

After inspecting L781-L812 of `beamerbaseauxtemplates.sty`:

```latex
\makeatletter
\defbeamertemplate{note page}{plainer}
{%
  \vskip4em
  \insertnote
}
\makeatother

\setbeamertemplate{note page}[plainer]
```

### Further customisation

[beamer - Note page showing the next frame - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/questions/33051/note-page-showing-the-next-frame)


## Presentation software

- [Cimbali/pympress](https://github.com/Cimbali/pympress/)
- [pdfpc/pdfpc](https://github.com/pdfpc/pdfpc)
- [Présentation.app](http://iihm.imag.fr/blanch/software/osx-presentation/) (No support for `\note`)
- [Skim](https://skim-app.sourceforge.io/)

Refs:

- [beamer - Is there a nice solution to get a "presenter mode" for Latex presentations? - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/questions/21777/is-there-a-nice-solution-to-get-a-presenter-mode-for-latex-presentations/)


## Remotely related: Markdown slideshows

- [astefanutti/decktape: PDF exporter for HTML presentations](https://github.com/astefanutti/decktape)
- [alexeygumirov/pandoc-beamer-how-to: Making presentations with Pandoc beamer](https://github.com/alexeygumirov/pandoc-beamer-how-to)
