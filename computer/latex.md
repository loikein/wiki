Most of time I only use LaTeX for maths.

## Spaces

Positive space: $$a\phantom{00000}b$$

```latex
a\phantom{00000}b
```

Negative space: $$\mkern12mu\not\mkern-24mu\iff$$ ([credit](https://tex.stackexchange.com/a/67913/206709))

```latex
% The first part is for stopping eating into contents before
\mkern12mu\not\mkern-24mu\iff
```

## Math Fonts

Bold: $$\mathbf{X}$$

```latex
\mathbf{X}
```

Bold hollow: $$\mathbb{R}$$

```latex
\mathbb{R}
```

Cursive: $$\mathcal{N}$$

```latex
\mathcal{N}
```

## Force Non-Display Size

Compare:

$$
\textstyle{\sum}_{i=1}^{10} i
$$

$$
\sum_{i=1}^{10} i
$$

```latex
\textstyle{\sum}_{i=1}^{10}

\sum_{i=1}^{10}
```

## Combining Symbols

Above: $$x\overset{!}{=}0$$

```latex
x\overset{!}{=}0
```

## Alignment

Cases: $$\begin{cases}x=1 & y=1\\ x=2 & y=2 \end{cases}$$

```latex
\begin{cases}x=1 & y=1\\ x=2 & y=2 \end{cases}
```

Equations: $$\begin{aligned}x &= 1 \\ abcde &= 2 \end{aligned}$$

```latex
\begin{aligned}x &= 1 \\ abcde &= 2 \end{aligned}
```

Spaces in equations: $$\begin{aligned} x &= 12345 \\ &\phantom{\ggg} + 67890\end{aligned}$$

```latex
\begin{aligned} x &= 12345 \\ &\phantom{\ggg} + 67890\end{aligned}
```
