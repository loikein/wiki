---
weight: 400
title: "espanso"
---


# espanso

Reference: [Documentation \- espanso \- Cross-platform Text Expander written in Rust](https://espanso.org/docs/)

## Basics

User profile path: `~/Library/Preferences/espanso/`  
Config file: `~/Library/Preferences/espanso/default.yml`

To find out about this:

```bash
$ espanso path
```

## Options

### `word:true`

The difference introduced when using `word: true` option is that you will need to type an extra space before expanding. For example, if you write this in `default.yml`:

```yaml
matches:
  - trigger: ":email"
    word: true
    replace: "example@example.com"
```

then you will result in `example@example.com␣` ending with a space, which may not be recognised as a valid email address on some websites. Therefore, you may want to not to use the option.

### `propagate_case: true`

When the replacement is a word with different cases, preserves the trigger's case.

The following trigger replaces ":btw" with "between", ":Btw" with "Between", and ":BTW" with "BETWEEN":

```yaml
  - trigger: ":btw"
    word: true
    propagate_case: true
    replace: "between"
```

### `$|$`

Places the cursor after replacing. See [\#Quick LaTeX Maths](#quick-latex-maths).

## Match Examples

### Reading Notes

```yaml
  - trigger: ":book"
    word: true
    replace: |
      ## Reading note

      - Time: {{mydate}}
      - Author:
      - Title:
      - Page:
      - Notes:
    vars:
      - name: mydate
        type: date
        params:
          format: "%Y%m%d%H%M"
```

### Quick Python Imports

```yaml
  - trigger: ":np"
    replace: "import numpy as np"
  - trigger: ":pd"
    replace: "import pandas as pd"
  - trigger: ":cp"
    replace: "import chaospy as cp"
```

### Quick LaTeX Maths

ref: [How I'm able to take notes in mathematics lectures using LaTeX and Vim \| Gilles Castel](https://castel.dev/post/lecture-notes-1/)

```yaml
  - trigger: ":mi"
    replace: "$$|$$"
  - trigger: ":mp"
    replace: |
      $$\begin{aligned}$|$ \end{aligned}$$
  - trigger: ":lim"
    replace: |
      \lim_{n \to \infty}
  - trigger: ":sum"
    replace: |
      \sum_{n=1}^{\infty}
```

### Breadcrumb Trail

Credit: [Fun with espanso \- Share & showcase \- Obsidian Forum](https://forum.obsidian.md/t/fun-with-espanso/2317)

```yaml
  - trigger: ":bc"
    word: true
    replace: "{{output}}"
    vars:
      - name: output
        type: shell
        params:
          cmd: "echo `date -v -1d \"+[[%Y-%m-%d|<< Yesterday]]\"`' | '`date -v +1d \"+[[%Y-%m-%d|Tommorrow >>]]\"`"
```
