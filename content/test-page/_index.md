---
bookCollapseSection: true
weight: 10
title: "Test pages"
---
[CommonMark Spec](https://spec.commonmark.org/)

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

<!-- ref: https://burk.io/2020/let-there-be-dark -->

<span title="#282a36" style="height: 30px; width: 90px; background-color: #282a36; display: inline-block; border-style: solid; border-color: black; color:white; padding-left: 5px; padding-right: 5px;">#282A36</span>

<span title="#f8f8f2" style="height: 30px; width: 90px; background-color: #f8f8f2; display: inline-block; border-style: solid; border-color: black; color:black; padding-left: 5px; padding-right: 5px;">#F8F8F2</span>

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

Usage:

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

Usage:

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

Usage:

```html
{{</* columns */>}}
Hello...

<--->

...hello...

<--->

...world.
{{</* /columns */>}}
```

### Summary/Detail

{{< details "Summary" open >}}
Who am I? Where am I?
{{< /details >}}

Usage:

```html
{{</* details "Summary" open */>}}
Who am I? Where am I?
{{</* /details */>}}
```

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

Usage:

```html
{{</* tabs "test-tabs" */>}}
{{</* tab "macOS" */>}} Ok {{</* /tab */>}}
{{</* tab "Linux" */>}} Ok {{</* /tab */>}}
{{</* tab "Windows" */>}} Not ok {{</* /tab */>}}
{{</* /tabs */>}}
```

TODO: Use [gohugoio/hugo/docs/layouts/shortcodes/code-toggle.html](https://github.com/gohugoio/hugo/blob/master/docs/layouts/shortcodes/code-toggle.html) with [gohugoio/hugoDocs/layouts/shortcodes/code-toggle.html](https://github.com/gohugoio/hugoDocs/blob/master/layouts/shortcodes/code-toggle.html) which has synced tab groups.


## Custom Shortcodes (by me)

### highlight-file

{{< highlight-file file="test.py" lang="python" >}}

Usage:

```html
{{</* highlight-file file="test.py" lang="python" */>}}
```

Folder structure: \(via [Hugo Page bundle](https://gohugo.io/content-management/page-bundles/)\)

> Non-page resources work for both branch bundles and leaf bundles. Therefore, so long as the highlighted file is not of [content formats](https://gohugo.io/content-management/formats/), it can be a resource for any page.
{.book-hint .info}

```text
content/test-page
├── _index.md     <-- branch bundle index file
└── test.py       <-- resource for section page: test-page

content/computer/software-usage/obsidian
├── index.md      <-- leaf bundle index file
└── theme-ib.css  <-- resource for regular page: obsidian
```

### kbd

{{< kbd I hate typing >}}　

Usage:

```html
{{</* kbd I hate typing */>}}

<!-- if key contains symbols, use literal -->
{{</* kbd `I` `hate` `typing` */>}}
```

### GitHub Gist

Native mode: \(No JS, with optional `lineNos` and `hlLines` params that work exactly like in the `highlight` shortcode.\)

{{< gist
user="loikein"
gist="27ef6913386b206d1b3c18b8e93c5768"
file="hello-world.md"
lang="markdown" >}}

Usage:

```html
{{</* gist
user="loikein"
gist="27ef6913386b206d1b3c18b8e93c5768"
file="hello-world.md"
lang="markdown"
lineNos="table"
hlLines="2-4 7" */>}}
```

Embed mode: \(No fallback for lack of JS, only use when you have to.\)

{{< gist
user="loikein"
gist="27ef6913386b206d1b3c18b8e93c5768"
file="hello-world.md"
syntax="markdown"
embed="true" >}}

Usage:

```html
{{</* gist
user="loikein"
gist="27ef6913386b206d1b3c18b8e93c5768"
file="hello-world.md"
syntax="markdown"
embed="true" */>}}
```

### ruby

{{< ruby "你好世界" "hello world" >}}

Usage:

```html
{{</* ruby "你好世界" "hello world" */>}}
```
