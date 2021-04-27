# Hugo/Blogdown

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

