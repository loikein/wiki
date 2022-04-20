# LaTeX Symbols

Big ref:

- [Detexify LaTeX handwritten symbol recognition](https://detexify.kirelabs.org/classify.html)
- The Comprehensive LaTeX Symbol List

## Logic

Ref: my brain

| Name | looks like | LaTeX |
|------|------------|------|
| Not | $$\lnot$$ | `\lnot` |
| And | $$\land$$ | `\land` |
| Or | $$\lor$$ | `\lor` |

## Arrows

Ref: my brain

| Name | looks like | LaTeX |
|------|------------|-------|
| Function to | $$\to$$ | `\to` |
| Map to | $$\mapsto$$ | `\mapsto` |
| Correspondence to | $$\rightrightarrows$$ | `\rightrightarrows` |
| If and only if | $$\iff$$ | `\iff` |
| If | $$\Longrightarrow$$ | `\Longrightarrow` |
| Only if | $$\implies$$ or $$\Longleftarrow$$ | `\implies` |

## Preference relations

Ref: [Symbols for Preference Relations - Oeconomist](https://www.oeconomist.com/blogs/daniel/wp-content/uploads/2011/04/pref_symbols.pdf)

| Name | looks like | LaTeX |
|------|------------|-------|
| Strictly prefer | $$\succ$$ | `\succ` |
| Not strictly preferred |  | `\not\succ` or `\nsucc` |
| Strictly worse | $$\prec$$ | `\prec` |
| Weakly prefer | $$\succsim$$ | `\succsim` |
| Not weakly preferred |  | `\not\succsim` |
| Weakly worse | $$\precsim$$ | `\precsim` |
| Indifferent | $$\sim$$ | `\sim` |
| Not indifferent |  | `\not\sim` or `\nsim` |
| Strict extension |  | `\rhd` |
| Weak extension | $$\unrhd$$ | `\unrhd` |

## Sets

Ref: [List of LaTeX mathematical symbols - OeisWiki](https://oeis.org/wiki/List_of_LaTeX_mathematical_symbols)

| Name | looks like | LaTeX |
|------|------------|-------|
| For all | $$\forall$$ | `\forall` |
| Exists | $$\exists$$ | `\exists` |
| Element | $$\in$$ | `\in` |
| Weak subset | $$\subseteq$$ | `\subseteq` |
| Strong subset | $$\subsetneqq$$ | `\subsetneqq` |
| Union | $$\cup$$ | `\cup` |
| Intersection | $$\cap$$ | `\cap` |

## Definitions

| Name | looks like | LaTeX | Ref|
|------|------------|-------|----|
| Is defined as | $$\coloneqq$$ | `\coloneqq` | [🔗](https://tex.stackexchange.com/a/4217) |
| Is equivalent to | $$\equiv$$ | `\equiv` | |
| Triangle equal | $$\triangleq$$ | `\triangleq` or `\overset{\Delta}{=}` | [🔗](https://tex.stackexchange.com/questions/163829/) |
| Set definition separations | $$\colon$$; $$\mid$$ | `\colon` and `\mid` | [🔗](https://tex.stackexchange.com/a/281551/) |

## Spaces

Ref: [Whitespace in math mode – texblog](https://texblog.org/2014/04/09/whitespace-in-math-mode/)

| Name | looks like | LaTeX |
|------|------------|-------|
| (No space) | $$a\rightarrow\leftarrow b$$ | / |
| Thin space | $$a\rightarrow\,\leftarrow b$$ | `\,` |
| Thin neq space | $$a\rightarrow\!\leftarrow b$$ | `\!` |
| Medium space | $$a\rightarrow\:\leftarrow b$$ | `\:` |
| Large space | $$a\rightarrow\;\leftarrow b$$ | `\;` |
| 1en space | $$a\rightarrow\enspace\leftarrow b$$ | `\enspace` |
| 1em space | $$a\rightarrow\quad\leftarrow b$$ | `\quad` |
| 2em space | $$a\rightarrow\qquad\leftarrow b$$ | `\qquad` |
| Custom em space | $$a\rightarrow\hspace{3em}\leftarrow b$$ | `\hspace{3em}` |

## Align environments

### Basic aligns & tag position

Ref: my brain

| Name | looks like | LaTeX |
|------|------------|-------|
| Equation | ![](/img/latex_equation.png) | `$...$` or `\begin{equation}\end{equation}` |
| Aligned single equation | ![](/img/latex_aligned.png) | `\begin{aligned}\end{aligned}` |
| Align multiple equation (no tag) | ![](/img/latex_align_star.png) | `\begin{align*}\end{align*}` |
| Align multiple equation (tagged) | ![](/img/latex_align.png) | `\begin{align}\end{align}` |
