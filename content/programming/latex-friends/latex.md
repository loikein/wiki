# LaTeX

Most of time I only use LaTeX for maths.

## Debugging (in Shell)

Find out the current version of LaTeX: \([credit](https://superuser.com/a/492743)\)

```bash
$ pdflatex --version
```

When `\xdef\@fontenc@load@list{\@fontenc@load@list undefined control sequence` happens: \([credit](https://stackoverflow.com/a/60493558/10668706)\)

```bash
$ fmtutil-sys --all
```

### Math Stuff

### Spaces

Positive space: $$a\phantom{00000}b$$

```text
a\phantom{00000}b
```

Negative space: $$\mkern12mu\not\mkern-24mu\iff$$ \([credit](https://tex.stackexchange.com/a/67913/206709)\)

```text
% The first part is for stopping eating into contents before
\mkern12mu\not\mkern-24mu\iff
```

### Math Fonts

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

### Force Non-Display Size

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

### Combining Symbols

Above: $$x\overset{!}{=}0$$

```text
x\overset{!}{=}0
```

## Align environments

### Basic aligns & tag position

Equation: `$$ ... \tag{1}$$` or `\begin{equation} ... \end{equation}`

![Equation  with tag](/img/latex_equation.png)

Aligned single equation: `\begin{aligned} ... \tag{2}\end{aligned}`

![Aligned single equation with tag](/img/latex_aligned.png)

Align multiple equation (no tag): `\begin{align*} ... \end{align*}`

![Align multiple equation with no tag](/img/latex_align_star.png)

Align multiple equation (tagged): `\begin{align} ... \end{align}`

![Align multiple equation with tag](/img/latex_align.png)

### More examples

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

