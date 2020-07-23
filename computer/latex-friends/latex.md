# LaTeX

Most of time I only use LaTeX for maths.

## Spaces

Positive space: $$a\phantom{00000}b$$

```text
a\phantom{00000}b
```

Negative space: $$\mkern12mu\not\mkern-24mu\iff$$ \([credit](https://tex.stackexchange.com/a/67913/206709)\)

```text
% The first part is for stopping eating into contents before
\mkern12mu\not\mkern-24mu\iff
```

## Math Fonts

Bold: $$\mathbf{X}$$

```text
\mathbf{X}
```

Bold hollow: $$\mathbb{R}$$

```text
\mathbb{R}
```

Cursive: $$\mathcal{N}$$

```text
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

```text
\textstyle{\sum}_{i=1}^{10}

\sum_{i=1}^{10}
```

## Combining Symbols

Above: $$x\overset{!}{=}0$$

```text
x\overset{!}{=}0
```

## Alignment

Cases: $$\begin{cases}x=1 & y=1\\ x=2 & y=2 \end{cases}$$

```text
\begin{cases}x=1 & y=1\\ x=2 & y=2 \end{cases}
```

Equations: $$\begin{aligned}x &= 1 \\ abcde &= 2 \end{aligned}$$

```text
\begin{aligned}x &= 1 \\ abcde &= 2 \end{aligned}
```

Spaces in equations: $$\begin{aligned} x &= 12345 \\ &\phantom{\ggg} + 67890\end{aligned}$$

```text
\begin{aligned} x &= 12345 \\ &\phantom{\ggg} + 67890\end{aligned}
```

Braces with multiple lines: $$\underbrace{abcdef}_{\begin{subarray}{l}\text{hello}\\\text{world}\end{subarray}}$$

```text
\underbrace{abcdef}_{\begin{subarray}{l}\text{hello}\\\text{world}\end{subarray}}
```
