---
weight: 200
title: "LaTeX Maths"
---

## Math Fonts

Ref: [Mathematical fonts - Overleaf, Online LaTeX Editor](https://www.overleaf.com/learn/latex/Mathematical_fonts)

Bold: `$\mathbf{RQSZN}$`, `$\mathbf{1}$`, `$\boldsymbol{\beta}$`

```latex
\mathbf{X}
\mathbf{1}
\boldsymbol{\beta}    % requires amsbsy package % https://tex.stackexchange.com/a/99286
```

Bold hollow: `$\mathbb{RQSZN}$` (for numbers [extra packages are needed](https://tex.stackexchange.com/a/583600))

```latex
\mathbb{R}
```

Cursive: `$\mathcal{RQSZN}$`

```latex
\mathcal{N}
```

## Force Non-Display Size

Compare:

`$$
\textstyle{\sum}_{i=1}^{10} i
$$`

`$$
\sum_{i=1}^{10} i
$$`

```latex
\textstyle{\sum}_{i=1}^{10}

\sum_{i=1}^{10}
```

## Combining Symbols

Above: `$x\overset{!}{=}0$`

```latex
x\overset{!}{=}0
```

With negative space: `$\mkern12mu\not\mkern-24mu\iff$` \([credit](https://tex.stackexchange.com/a/67913/206709); [another way not supported by KaTeX](https://tex.stackexchange.com/a/75362)\)

```latex
% The first part is for stopping eating into contents before
\mkern12mu\not\mkern-24mu\iff

% or
\usepackage{centernot}
\centernot\iff
```


## Better `\bar`

Ref: [stacking symbols - The \bar and \overline commands - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/a/22134)

Gives the middle one:

![](https://i.stack.imgur.com/kN66B.png)

```latex
\usepackage{amsfonts}
\newcommand{\overbar}[1]{\mkern 1.5mu\overline{\mkern-1.5mu#1\mkern-1.5mu}\mkern 1.5mu}

$\overbar{\mathbb{R}}$
```

## Alignment

### Basic aligns & tag position

#### Single line equation

{{< details "With `\label{eq1}`, you can refer to it as [eq1](#eq1); `$\eqref{eq1}$`; `$\ref{eq1}$`" >}}
…by typing:

```markdown
[eq1](#eq1); $\eqref{eq1}$; $\ref{eq1}$
```

The latter two are valid in LaTeX as well.

This requires adding macros when importing KaTeX. See [Issue #2003 · KaTeX/KaTeX](https://github.com/KaTeX/KaTeX/issues/2003#issuecomment-843991794) for details.

There is also [`\htmlId` functionality](https://katex.org/docs/supported.html#html) which is less intuitive to use but do not require adding macros.
{{< /details >}}

Auto tagged: \(Numbers are continuous during the whole webpage\)

`$$\begin{equation} x = y \label{eq1}\end{equation}$$`

```latex
\begin{equation} x = y \label{eq1}\end{equation}
```

> To avoid overflow in KaTeX, you can also avoid `equation` or `equation*` environments, and manually tag it: \(Numbers are not continuous\)
> 
> `$$x = y \label{eq1.1}\tag{1.1}$$`
> 
> ```latex
> x = y \label{eq1.1}\tag{1.1}
> ```
{.book-hint .info}

No tag:

`$$\begin{equation*} x = y \end{equation*}$$`

```latex
\begin{equation*} x = y \end{equation*}
```

#### Multi-line signle equation with `aligned`

Auto tagged:

`$$
\begin{equation}
\begin{aligned}
  x &= y \\
  &= z
\end{aligned}
\end{equation}$$`

```latex
\begin{equation}
\begin{aligned}
  x &= y \\
  &= z
\end{aligned}
\end{equation}
```

<!-- ![Aligned single equations with tag](/img/latex_aligned.png) -->

> To avoid overflow in KaTeX, manual tag it:
> 
> `$$
> \begin{aligned}
>   x &= y \\
>   &= z \tag{2.1}
> \end{aligned}
> $$`
> 
> ```latex
> \begin{aligned}
>   x &= y \\
>   &= z \tag{2.1}
> \end{aligned}
> ```
{.book-hint .info}

#### Multiple equations with `Align`

Auto tagged:

`$$\begin{align} x &= y \\ 2x &= 2z \end{align}$$`

```latex
\begin{align} x &= y \\ 2x &= 2z \end{align}
```

> I have yet to find any way to avoid tag overflow for `align` environments for KaTeX.
{.book-hint .warning}

No tag:

`$$\begin{align*} x &= y \\ 2x &= 2z \end{align*}$$`

<!-- ![Align multiple equations with no tag](/img/latex_align_star.png) -->

```latex
\begin{align*} x &= y \\ 2x &= 2z \end{align*}
```


### More examples

Cases:

`$$
\begin{cases}
  x=1 & y=1\\
  x=2 & y=2
\end{cases}
$$`

```latex
\begin{cases}
  x=1 & y=1\\
  x=2 & y=2
\end{cases}
```

Symbols as equation tag: \([Ref](https://tex.stackexchange.com/questions/12026/)\)

`$$E=mc^2 \tag{$*$}$$`

```latex
E=mc^2 \tag{$*$}
```

Spaces in equations:

`$$\begin{aligned} x &= 12345 \\ &\phantom{\ggg} + 67890\end{aligned}$$`

```latex
\begin{aligned} x &= 12345 \\ &\phantom{\ggg} + 67890\end{aligned}
```

Braces with multiple lines:

`$$\underbrace{abcdef}_{\begin{subarray}{l}\text{hello}\\\text{world}\end{subarray}}$$`

```latex
\underbrace{abcdef}_{\begin{subarray}{l}\text{hello}\\\text{world}\end{subarray}}
```

Aligned braces: \([Ref](https://tex.stackexchange.com/a/585309)\)

`$$ f(x,z) = \underbrace{\int^a_b x\ dx}_{\text{Things}} + \underbrace{\vphantom{\int_b}2333z}_{\text{More things}} $$`

```latex
f(x,z) = \underbrace{\int^a_b x\ dx}_{\text{Things}}
 +\underbrace{\vphantom{\int_b}2333z}_{\text{More things}}
```

More aligned braces: \([Ref](https://tex.stackexchange.com/a/46311)\)

`$$
f(x,z) = \underbrace{\int^a_b x\ dx}_{\text{Things}} 
+\overbrace{\vphantom{\int^a}42xz^2}^{\mathclap{\text{Longer other things}}}
+\underbrace{\vphantom{\int_b}2333z}_{\mathclap{\text{More longer things}}}
$$`

```latex
f(x,z) = \underbrace{\int^a_b x\ dx}_{\text{Things}} 
 +\overbrace{\vphantom{\int^a}42xz^2}^{\mathclap{\text{Longer other things}}}
 +\underbrace{\vphantom{\int_b}2333z}_{\mathclap{\text{More longer things}}}
```


## Newer and better environment defaults

### Space in braces

Refs:

- [math mode - How to adjust the blank space between the top of the left curly brace and the contents? - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/a/115228)
- [Horizontal spacing after cases bracket in equation - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/a/173086)

```latex
\usepackage{amsmath}
\makeatletter
\def\env@cases{%
  \let\@ifnextchar\new@ifnextchar
  \left\lbrace
  \def\arraystretch{1.1}%
  \array{@{\,}l@{\quad}l@{}}%
}
\makeatother
```
