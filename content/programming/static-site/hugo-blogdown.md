---
title: "Hugo/Blogdown"
disable_latex: true
---

## Basics

Doc: [Quick Start | Hugo](https://gohugo.io/getting-started/quick-start/)

```sh
# Start fresh
hugo new site mysite && cd mysite

# Serve local site (including drafts)
hugo server --buildDrafts --disableFastRender

# Build example site of theme
cd exampleSite && hugo server --buildDrafts --themesDir .. --theme .
```

## Useful commands

Doc: [hugo | Hugo](https://gohugo.io/commands/hugo/#options)

### Local

```sh
# run local server with drafts
hugo server --buildDrafts

# rebuild every time
# warning: changes too layout files still need restarting server
--disableFastRender

# log time used
--logLevel info

# log template usage and caching potentials
--templateMetrics --templateMetricsHints

# check path clashes
--printPathWarnings
```

### Deploy

Battle-tested deployment commands

```sh
# For whole site
hugo --gc --minify

# For site with pagefind
hugo --gc --minify && npm_config_yes=true npx pagefind --source 'public'

# For theme with example site
cd exampleSite && hugo --gc --minify --themesDir .. --theme .
```

## Useful shortcuts

### Timestamped draft filenames

Create new post with date & time in the filename: ([credit](https://discourse.gohugo.io/t/dates-in-post-filenames/26219/7))

```sh
hugo new drafts/$(date +"%Y-%m-%d")-draft$(date +"%H%M%S").md
```

Timestamp: ([credit](https://unix.stackexchange.com/a/629504))

```sh
date +"%Y-%m-%dT%H:%M:%S%z"
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

### Regex for search and replace HTML comment with GoHTML comment

Find
: `(<!--)(.*)(-->)`

Replace
: `{{/\*\2\*/}}`

## Custom CSS

### Site-wide

Blog: [如何在 Hugo 中添加自定义 CSS - 此生未命名／Untitled Life](https://playground.loikein.one/hugo-diary-public/posts/2021-04-26-hugo-custom-css-the-right-way/)

Layout: (`layouts/partials/head.html`)

```go-html-template
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

```text
assets
└── css
    ├── 1.css
    └── 2.css
```

### Single page

Ref: [Using an additional specific css style for a page - HUGO](https://discourse.gohugo.io/t/using-an-additional-specific-css-style-for-a-page/26547)

Layout: (`layouts/partials/head.html`)

```go-html-template
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

File tree: \(using [page bundle](https://gohugo.io/content-management/page-bundles/)\)

```text
content
└── posts
    └── some-random-post
        ├── index.md
        └── test.css
```


## Search with pagefind

Remember to:

1. Add search layout and link to search page;
2. Update deployment commands

Example: [loikein/blog-hugo@6891567](https://github.com/loikein/blog-hugo/commit/6891567c28f6af18976ce433b53ad64f90b93b0e), [loikein/blog-hugo@ef52aef](https://github.com/loikein/blog-hugo/commit/ef52aefbc1af8a2243823c46c49641b625967ff2)

On local:

```sh
# first, add /public to .gitignore
echo "/public/" >> .gitignore
echo  "static/_pagefind" >> .gitignore

# then, build and generate pagefind index
hugo && npm_config_yes=true npx pagefind --source "public"

# finally, run local server
hugo server --buildDrafts --disableFastRender
```

## Blogdown basics

> I have stopped using Blogdown. Proceed at your own risk.
{.book-hint .danger}

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
2. Add TOC to layout: in `site/themes/hugo-theme/layouts/_default/single.html`, add:

```go-html-template {hl_lines="2-4"}
<div class="article-content">
  {{- if ne .Params.toc false -}}
  <div id="TOC">{{ .TableOfContents }}</div>
  {{- end -}}
  {{ .Content }}
</div>
```

> I just cannot make the `output - blogdown::html_page: - toc` param work seamlessly after many tries. Maybe it was because of the colons.
{.book-hint .warning}

**Step 3. Markdown, HTML & Config  changes**

1. Footnotes are inline \(`^[…]`\), which is [not supported by goldmark](https://github.com/yuin/goldmark/issues/47).
1. All titles used to be `<div><h?>…</h?></div>`, now are just `<h?>…</h?>`.
1. Code blocks may appear weird because Blogdown used highlight.js. Add `markup: highlight: codeFences: false` in `config.yaml` \(per [wowchemy/wowchemy-hugo-themes Issue #1496](https://github.com/wowchemy/wowchemy-hugo-themes/issues/1496)\).

**Step 4. Keep track of LaTeX in .md files**

1. Make sure to check `themes/hugo-theme/static/js/math-code.js`.
    1. Bonus: add `nolatex` inline fix ([L5 of loikein/hugo-book/assets/latex-fix.js](https://github.com/loikein/hugo-book/blob/master/assets/latex-fix.js#L5))
    2. Bonus: add per-page `.Params.disable_latex` check for loading LaTeX renderer ([L1 of loikein/hugo-book/layouts/partials/docs/footer-katex.html](https://github.com/loikein/hugo-book/blob/master/layouts/partials/docs/footer-katex.html#L1))
2. Note that any `- `, `+ `, or `> ` at beginnings of lines will break the LaTeX block it is in. Need to remove those spaces. (A not-very-good-RegEx for this: ``(`\$\$)((.*\n)*)(-\s.*)((.*\n)*)(\$\$`)``)
3. There are cases where the LaTeX code lose the `` ` `` (around or on one side of them) consistently. Need to check for those: \(best way is on Hugo local server\)
    - LaTeX surrounded by space (e.g. starts with `␣$$` or ends with `$$␣`)
    - LaTeX surrounded by brackets (e.g. starts with `($$`, `($`, or `(\(`; or ends with `$$)`, `$)`, or `\))`)

**Step 5. Debugging for Netlify**

1. I had to remove the following files to resolve Netlify building error: `Failed during stage 'preparing repo': error checking for ref: refs/heads/hugo: : exit status 2`

```text
 7 files changed, 131 deletions(-)
 delete mode 100644 .Rhistory
 delete mode 100644 .Rprofile
 delete mode 100644 R/build.R
 delete mode 100644 blogdown-site.Rproj
 delete mode 100644 content/post/.Rhistory
 delete mode 100644 ignored/static-writings/Makefile
 delete mode 100644 ignored/static-writings/_render.R
```

**Step 6. Done!**


