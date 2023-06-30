---
title: "Hugo/Blogdown"
---

## Hugo basics

[Quick Start | Hugo](https://gohugo.io/getting-started/quick-start/)

```bash
$ hugo new site mysite
$ cd mysite

# Serve local site (live reload)
$ hugo server

# (including drafts)
$ hugo server --buildDrafts

# (greedy loading mode)
$ hugo server --disableFastRender

# Build site
$ hugo
```

### Useful shortcuts

Create new post with date & time in the filename: ([credit](https://discourse.gohugo.io/t/dates-in-post-filenames/26219/7))

```bash
$ hugo new drafts/$(date +"%Y-%m-%d")-draft$(date +"%H%M%S").md
```

Timestamp: ([credit](https://unix.stackexchange.com/a/629504))

```bash
$ date +"%Y-%m-%dT%H:%M:%S%z"
```

My [espanso](/computer/software-usage/espanso.md) triggers just for reference:

```yaml
  - trigger: ":stamp"
    replace: "{{iso}}"
    vars:
      - name: iso
        type: date
        params:
          format: "%Y-%m-%dT%H:%M:%S%z"

  - trigger: ":hugonew"
    replace: |
      hugo new drafts/$(date +"%Y-%m-%d")-draft$(date +"%H%M%S").md
```

## Blogdown basics

{{< hint warning >}}
I have not used Blogdown for a long time. Proceed at your own risk.
{{< /hint >}}

Install:

```r
blogdown::install_hugo()
blogdown::hugo_version()

blogdown::new_site()
file.edit("~/.Rprofile")
blogdown:::serve_site()
blogdown::new_post()

blogdown::install_theme("xianmin/hugo-theme-jane")
## blogdown::install_theme("loikein/hugo-lithium-loikein", force=T)
```

## Migrate from Blogdown to Hugo

**Step 1. Get .md version of all .Rmd files**

1. Delete all .html files in `site/content/`; delete the `site/public/` folder
2. Add `options(blogdown.method = "markdown")` to `site/.Rprofile`
3. Restart R (`quit()`)
4. Run `blogdown::serve_site()` (slow if you have a lot of pages)
5. After the run finishes, run `blogdown::stop_server()`

**Step 2. Test on local Hugo server**

1. Add `ignoreFiles: - ".Rmd$"` to `site/config.yaml`
2. Add TOC: in `site/themes/hugo-theme/layouts/_default/single.html`, add:

```html {hl_lines="2-4"}
    <div class="article-content">
      {{- if ne .Params.toc false -}}
      <div id="TOC">{{ .TableOfContents }}</div>
      {{- end -}}
      {{ .Content }}
    </div>
```

{{< hint warning >}}
I just cannot make the `output - blogdown::html_page: - toc` param work seamlessly after many tries.
{{< /hint >}}

**Step 3. Adjust CSS**

1. CSS for code blocks may appear weird

**Step 4. Keep track of LaTeX**

1. `latex-fix.js`
2. Note that any `- `, `+ `, or `> ` at beginnings of lines will break the LaTeX block it is in. Need to remove those spaces. (A not-very-good-RegEx for this: ``(`\$\$)((.*\n)*)(-\s.*)((.*\n)*)(\$\$`)``)
3. There are cases where the LaTeX code lose the `` ` `` (around or on one side of them) consistently. Need to check for those: \(best way is on Hugo local server\)
    - LaTeX surrounded by space (e.g. starts with <code class="nolatex"> $$</code> or ends with <code class="nolatex">$$ </code>)
    - LaTeX surrounded by brackets (e.g. starts with <code class="nolatex">($$</code>, <code class="nolatex">($</code>, or <code class="nolatex">(\(</code>; or ends with <code class="nolatex">$$)</code>, <code class="nolatex">$)</code>, or <code class="nolatex">\))</code>)


**Step 5. Done!**


## Add custom CSS (site)

过程：[如何在 Hugo 中添加自定义 CSS - 此生未命名／Untitled Life](https://playground.loikein.one/hugo-diary-public/posts/2021-04-26-hugo-custom-css-the-right-way/)

Layout: (`layouts/partials/head.html`)

```html
{{ if .Site.Params.customCSS }}
{{ $style := resources.Match "css/**.css" | resources.Concat "custom.css" | minify | fingerprint }}
<link rel="stylesheet" href="{{ $style.Permalink }}" integrity="{{ $style.Data.Integrity }}" media="screen">
{{ end }}
```

`config.yaml`:

```yaml
params:
  customCSS: true
```

File tree:

```
assets
└── css
    ├── 1.css
    └── 2.css
```

## Add custom CSS (single page)

Ref: [Using an additional specific css style for a page - HUGO](https://discourse.gohugo.io/t/using-an-additional-specific-css-style-for-a-page/26547)

Layout: (`layouts/partials/head.html`)

```html
{{ with $.Resources.GetMatch "**.css*" }}
{{ $style := . | minify | fingerprint }}
<link rel="stylesheet" href="{{ $style.Permalink }}" integrity="{{ $style.Data.Integrity }}" media="screen">
{{ end }}
```

Front matter:

```yaml
resources:
  - src: test.css
    title: style
```

File tree:

```
content
└── posts
    └── some-random-post
        ├── index.md
        └── test.css
```

