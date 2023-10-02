---
weight: 300
title: "Symbols"
---

## \(Maybe\) Useful resources

- [Detexify LaTeX handwritten symbol recognition](https://detexify.kirelabs.org/classify.html)
- [The Comprehensive LaTeX Symbol List](https://ctan.org/pkg/comprehensive)
- [Special LaTeX characters | TeXblog](https://texblog.net/latex-archive/uncategorized/symbols/)
- [Some thoughts on lowering the learning curve for using TeX (part I) | Random Determinism](https://randomdeterminism.wordpress.com/2011/09/04/some-thoughts-on-lowering-the-learning-curve-for-using-tex-part-i/)


## Symbols outside math mode

| Name | looks like | LaTeX | Notes |
|------|------------|-------|-------|
| Vertical bar | `$\text{\textbar}$` | `\textbar` | Needs a space after it `\textbar\,` |
| Percent sign | `$\%$` | `\%` |  |
| Hash sign    | `$\#$` | `\#` |  |
| Underscore   | `$\_$` | `\_` or `\textunderscore` |  |
| Tilde        | ``$\char`\~$`` | ``\char`\~`` | Plain TeX | 

## Logic

Ref: my brain

| Name | looks like | LaTeX |
|------|------------|------|
| Not | `$\lnot$` | `\lnot` |
| And | `$\land$` | `\land` |
| Or | `$\lor$` | `\lor` |

## Arrows

Ref: my brain

| Name | looks like | LaTeX |
|------|------------|-------|
| Function to | `$\to$` | `\to` |
| Map to | `$\mapsto$` | `\mapsto` |
| Correspondence to | `$\rightrightarrows$`  | `\rightrightarrows` |
| If and only if | `$\iff$` | `\iff` |
| If | `$\Longleftarrow$` | `\Longleftarrow` |
| Only if | `$\implies$` or `$\Longrightarrow$` | `\implies` or `\Longrightarrow` |

## Preference relations

Ref: [Symbols for Preference Relations - Oeconomist](https://www.oeconomist.com/blogs/daniel/wp-content/uploads/2011/04/pref_symbols.pdf)

| Name | looks like | LaTeX |
|------|------------|-------|
| Strictly prefer | `$\succ$` | `\succ` |
| Not strictly preferred | `$\not\succ$` | `\not\succ` or `\nsucc` |
| Strictly worse | `$\prec$` | `\prec` |
| Weakly prefer | `$\succsim$` | `\succsim` |
| Not weakly preferred | `$\not\succsim$` | `\not\succsim` |
| Weakly worse | `$\precsim$` | `\precsim` |
| Indifferent | `$\sim$` | `\sim` |
| Not indifferent | `$\not\sim$` | `\not\sim` or `\nsim` |
| Strict extension | `$\rhd$` | `\rhd` |
| Weak extension | `$\unrhd$` | `\unrhd` |

## Sets

Ref: [List of LaTeX mathematical symbols - OeisWiki](https://oeis.org/wiki/List_of_LaTeX_mathematical_symbols)

| Name | looks like | LaTeX |
|------|------------|-------|
| For all | `$\forall$` | `\forall` |
| Exists | `$\exists$` | `\exists` |
| Element | `$\in$` | `\in` |
| Weak subset | `$\subseteq$` | `\subseteq` |
| Strong subset | `$\subsetneqq$` | `\subsetneqq` |
| Union | `$\cup$` | `\cup` |
| Intersection | `$\cap$` | `\cap` |

## Definitions

| Name | looks like | LaTeX | Ref|
|------|------------|-------|----|
| Is defined as | `$\coloneqq$` | `\coloneqq` | [🔗](https://tex.stackexchange.com/a/4217) |
| Is equivalent to | `$\equiv$` | `\equiv` | |
| Triangle equal | `$\triangleq$` | `\triangleq` or `\overset{\Delta}{=}` | [🔗](https://tex.stackexchange.com/questions/163829/) |
| Set definition separations | `$\colon$` and `$\mid$` | `\colon` and `\mid` | [🔗](https://tex.stackexchange.com/a/281551/) |

## Spaces

Refs: 

- [Whitespace in math mode – texblog](https://texblog.org/2014/04/09/whitespace-in-math-mode/)
- [What commands are there for horizontal spacing? - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/a/74354)

| Name | looks like | LaTeX |
|------|------------|-------|
| Thin negative space | `$a\rightarrow\!\leftarrow b$` | `\!` |
| (No space) | `$a\rightarrow\leftarrow b$` | (Nothing) |
| Thin space | `$a\rightarrow\,\leftarrow b$` | `\,` |
| Medium space | `$a\rightarrow\:\leftarrow b$` | `\:` |
| Large space | `$a\rightarrow\;\leftarrow b$` | `\;` |
| 1en space | `$a\rightarrow\enspace\leftarrow b$` | `\enspace` |
| 1em space | `$a\rightarrow\quad\leftarrow b$` | `\quad` |
| 2em space | `$a\rightarrow\qquad\leftarrow b$` | `\qquad` |
| Custom em space | `$a\rightarrow\hspace{3em}\leftarrow b$` | `\hspace{3em}` |
| Custom words space | `$a\rightarrow\phantom{00000}\leftarrow b$` | `\phantom{00000}` |
