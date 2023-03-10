---
weight: 200
title: "LaTeX Maths"
---

# LaTeX Maths

## Math Fonts

Bold: `$\mathbf{X}$` `$\mathbf{1}$`

```text
\mathbf{X}
```

Bold hollow: `$\mathbb{R}$`

```text
\mathbb{R}
```

Cursive: `$\mathcal{N}$`

```text
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

```text
\textstyle{\sum}_{i=1}^{10}

\sum_{i=1}^{10}
```

## Combining Symbols

Above: `$x\overset{!}{=}0$`

```text
x\overset{!}{=}0
```

With negative space: `$\mkern12mu\not\mkern-24mu\iff$` \([credit](https://tex.stackexchange.com/a/67913/206709)\)

```text
% The first part is for stopping eating into contents before
\mkern12mu\not\mkern-24mu\iff
```

## Alignment

### Basic aligns & tag position

Equation: <code class="nolatex">$ ... \tag{1}$</code>  or <code class="nolatex">\begin{equation} ... \end{equation}</code>

![Equation  with tag](/img/latex_equation.png)

Aligned single equation: <code class="nolatex">\begin{aligned} ... \tag{2}\end{aligned}</code>

![Aligned single equations with tag](/img/latex_aligned.png)

Align multiple equations (no tag): <code class="nolatex">\begin{align*} ... \end{align*}</code>

![Align multiple equations with no tag](/img/latex_align_star.png)

Align multiple equations (tagged): <code class="nolatex">\begin{align} ... \end{align}</code>

![Align multiple equations with tag](/img/latex_align.png)

### More examples

Cases:

`$$
\begin{cases}x=1 & y=1\\ x=2 & y=2 \end{cases}
$$`

```text
\begin{cases}x=1 & y=1\\ x=2 & y=2 \end{cases}
```

Equations: 

`$$\begin{aligned}x &= 1 \\ abcde &= 2 \end{aligned}$$`

```text
\begin{aligned}x &= 1 \\ abcde &= 2 \end{aligned}
```

Spaces in equations:

`$$\begin{aligned} x &= 12345 \\ &\phantom{\ggg} + 67890\end{aligned}$$`

```text
\begin{aligned} x &= 12345 \\ &\phantom{\ggg} + 67890\end{aligned}
```

Braces with multiple lines:

`$$\underbrace{abcdef}_{\begin{subarray}{l}\text{hello}\\\text{world}\end{subarray}}$$`

```text
\underbrace{abcdef}_{\begin{subarray}{l}\text{hello}\\\text{world}\end{subarray}}
```

