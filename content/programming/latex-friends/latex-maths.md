---
weight: 200
title: "LaTeX Maths"
---

# LaTeX Maths

## Math Fonts

Ref: [Mathematical fonts - Overleaf, Online LaTeX Editor](https://www.overleaf.com/learn/latex/Mathematical_fonts)

Bold: `$\mathbf{RQSZN}$`, `$\mathbf{1}$`

```latex
\mathbf{X}
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

Single line equation: (Backref with [KaTeX quirks](https://github.com/KaTeX/KaTeX/issues/2003#issuecomment-843991794): [eq1](/programming/latex-friends/latex-maths/#eq1))


`$$\begin{equation} x = y \label{eq1}\end{equation}$$`

```latex
\begin{equation} x = y \label{eq1}\end{equation}
```

<!-- `$$x = y \tag{1.1}$$`

```latex
$$x = y \label{eq1.1}\tag{1.1}$$
``` -->

<!-- ![Equation  with tag](/img/latex_equation.png) -->

Aligned single equation:

`$$\begin{aligned} x &= y \\ &= z \tag{1.1}\end{aligned}$$`

<!-- ![Aligned single equations with tag](/img/latex_aligned.png) -->

```latex
\begin{aligned} x &= y \\ &= z \tag{1.1}\end{aligned}
```

Align multiple equations (no tag):

`$$\begin{align*} x &= y \\ x &= z \end{align*}$$`

<!-- ![Align multiple equations with no tag](/img/latex_align_star.png) -->

```latex
\begin{align*} x &= y \\ x &= z \end{align*}
```

Align multiple equations (tagged):

`$$\begin{align} x &= y \\ x &= z \end{align}$$`

<!-- ![Align multiple equations with tag](/img/latex_align.png) -->

```latex
\begin{align} x &= y \\ x &= z \end{align}
```

### More examples

Cases:

`$$
\begin{cases}x=1 & y=1\\ x=2 & y=2 \end{cases}
$$`

```latex
\begin{cases}x=1 & y=1\\ x=2 & y=2 \end{cases}
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

`$$ f(x,z) = \underbrace{\int^a_b x\ dx}_{\text{Things}} + \underbrace{\vphantom{\int_b}2333z}_{\text{Other things}} $$`

```latex
f(x,z) = \underbrace{\int^a_b x\ dx}_{\text{Things}}
 +\underbrace{\vphantom{\int_b}2333z}_{\text{Other things}}
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
