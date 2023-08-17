---
weight: 10
title: "Markdown tests"
---

## Normal tests

Begin [test file](https://gist.github.com/loikein/27ef6913386b206d1b3c18b8e93c5768)…

### Formatting

**Bold**, __bold__, **加粗**

*Italic*, _italic_, *斜体*

<u>Underline</u>, <underline>underline</underline>

<del>Strike</del>, <s>strike</s>, ~~strike~~, ~strike~, --strike--

<mark>Highlight</mark>, =highlight=, ==highlight==

<!-- Comments-->

Footnote[^1], footnote[^2]

[^1]: The linked footnote appears at the end of the document.

[^2]: New lines

---


### Lists

- `ul`
- Unordered list

1. `ol`
1. Ordered list

`dl`
:   `dt`
:   Description list

- [x] Task list
- [ ] Task list

### Code

Inline `code`, `` `escape` ``, and <kbd>keystroke</kbd>

Inline `code`, `` `escape` ``, and <kbd>keystroke</kbd>

```go {hl_lines=["2-5"],linenostart=199}
package main

import "log"

func add(x int, y int) int {
  log.Println("We are going to take the sum of two numbers, and leave a very very very long comment.")
  return x + y
}

func main() {
  y := add(1, 2)
  log.Println(y)
}
```

Here's an example with line numbers. The CSS is buggy.

```go {linenos=table,hl_lines=["2-5"],linenostart=199}
package main

import "log"

func add(x int, y int) int {
  log.Println("We are going to take the sum of two numbers, and leave a long comment.")
  return x + y
}

func main() {
  y := add(1, 2)
  log.Println(y)
}
```

### Font

> 我能体に傷つけないで吞下 259 ml glass。

> Four score and seven years ago our fathers brought forth upon this continent, a new nation, conceived in Liberty, and dedicated to the proposition that all men are created equal.

0 Oo Ii Ll 1 | 2 Z 5 s 8 Bb 6 # * ^ ~ \(\) {} \[\] . , : ; “ ‘ ’ \`

```
0 Oo Ii Ll 1 | 2 Z 5 s 8 Bb 6 # * ^ ~ () {} [] . , : ; “ ‘ ’ `
```

### Inline HTML

ref: https://burk.io/2020/let-there-be-dark

<div title="#282a36" style="height: 50px; width: 100px; background-color: #282a36; display: inline-block; border-style: solid; border-color: black; color:white; padding:10px;">#282a36</div>

<div title="#f8f8f2" style="height: 50px; width: 100px; background-color: #f8f8f2; margin-right: 5px; display: inline-block; border-style: solid; border-color: black; color:black; padding:10px;">#f8f8f2</div>

### LaTeX & Table

`$\LaTeX{}$`

`$$R_1 \begin{cases} >\mu_{2} \\ \leq \mu_{2} \end{cases}$$`

| Message to agent 1 | `$M_1$`          |
| ------------------ | -------------- |
| Agent 1's action   | `$a_1$`          |
| New finding        | `$R_1 \begin{cases} >\mu_{2} \\ \leq \mu_{2} \end{cases}$` |


### Hints with block attribute

CommonMark/Goldmark flavour: \(Doc: [#Attributes in yuin/goldmark/README](https://github.com/yuin/goldmark/#attributes)\)

> Info hint
{.book-hint .info}

> Warning hint
{.book-hint .warning}

> Danger **(!)** hint
{.book-hint .danger}

```markdown
> Info hint
{.book-hint .info}

> Warning hint
{.book-hint .warning}

> Danger **(!)** hint
{.book-hint .danger}
```

GitHub flavour: \(Doc: [[Markdown] An option to highlight a "Note" and "Warning" using blockquote (Beta) · community · Discussion #16925](https://github.com/orgs/community/discussions/16925)\)

> [!NOTE]  
> Highlights information that users should take into account, even when skimming.

> [!IMPORTANT]  
> Crucial information necessary for users to succeed.

> [!WARNING]  
> Critical content demanding immediate user attention due to potential risks.


```markdown
> [!NOTE]  
> Highlights information that users should take into account, even when skimming.

> [!IMPORTANT]  
> Crucial information necessary for users to succeed.

> [!WARNING]  
> Critical content demanding immediate user attention due to potential risks.
```



## Custom Shortcodes (by theme)

### Columns

{{< columns >}}
Hello...

<--->

...hello...

<--->

...world.
{{< /columns >}}

### Summary/Detail

{{< details "Summary" open >}}
Who am I? Where am I?
{{< /details >}}

### Hints \(deprecated\)

> Note: this has become redundant since Hugo v0.108.0 \([release notes](https://github.com/gohugoio/hugo/releases/tag/v0.108.0)\). Use [block attributes](#hints-with-block-attribute) instead.
> 
> See [Markdown attributes - tips & tricks - HUGO](https://discourse.gohugo.io/t/markdown-attributes/41783) for more info.
{.book-hint .info}

Previous usage:

```html
{{</* hint info */>}}
Info hint
{{</* /hint */>}}
```

```html
{{</* hint warning */>}}
Warning hint
{{</* /hint */>}}
```

```html
{{</* hint danger */>}}
Danger **(!)** hint
{{</* /hint */>}}
```

### Tabs

{{< tabs "test-tabs" >}}
{{< tab "macOS" >}} Ok {{< /tab >}}
{{< tab "Linux" >}} Ok {{< /tab >}}
{{< tab "Windows" >}} Not ok {{< /tab >}}
{{< /tabs >}}


## Custom Shortcodes (by me)

### kbd

{{< kbd I hate typing >}}　

```html
{{</* kbd I hate typing */>}}
```

### GitHub Gist

Native mode \(no JS\): (with optional `lineNos` and `hlLines` params that works exactly like `highlight` shortcode)

{{< gist
user="loikein"
gist="27ef6913386b206d1b3c18b8e93c5768"
file="hello-world.md"
lang="markdown" >}}

```html
{{</* gist
user="loikein"
gist="27ef6913386b206d1b3c18b8e93c5768"
file="hello-world.md"
lang="markdown"
lineNos="table"
hlLines="2-4 7" */>}}
```

Embed mode:

{{< gist
user="loikein"
gist="27ef6913386b206d1b3c18b8e93c5768"
file="hello-world.md"
syntax="markdown"
embed="true" >}}

```html
{{</* gist
user="loikein"
gist="27ef6913386b206d1b3c18b8e93c5768"
file="hello-world.md"
syntax="markdown"
embed="true" */>}}
```
