---
bookCollapseSection: true
title: CSS
---

My notes on CSS & HTML from ages ago \(in Japanese\): [notes: html 5 & css 3](https://gist.github.com/loikein/8af785feed5a265ca0cd936299178902)


## Font

### `@font-face`

Doc: [@font-face - CSS: Cascading Style Sheets | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face)

### `font-family` \(font stack\)

> Reminder to self: Remove `Segoe UI` from all font stacks.
{.book-hint .info}

### Google Fonts API

> [Google Fonts was deemed not GDPR compliant in Germany](https://rewis.io/urteile/urteil/lhm-20-01-2022-3-o-1749320/) \([coverage by The Hacker News](https://thehackernews.com/2022/01/german-court-rules-websites-embedding.html), [Bitdefender](https://www.bitdefender.com/blog/hotforsecurity/german-website-fined-100-euros-after-court-says-googles-font-library-violates-gdpr/), [jsDelivr](https://www.jsdelivr.com/blog/how-the-german-courts-ruling-on-google-fonts-affects-jsdelivr-and-why-it-is-safe-to-use/)\). If your website have a lot of visitors from the EU, consider self-hosting the fonts.
{.book-hint .danger}

#### Async \(v1\)

Refs:

- [The Fastest Google Fonts – CSS Wizardry – Web Performance Optimisation](https://csswizardry.com/2020/05/the-fastest-google-fonts/#google-fonts-async-snippet)
- [How to Load Fonts in a Way That Fights FOUT and Makes Lighthouse Happy | CSS-Tricks - CSS-Tricks](https://css-tricks.com/how-to-load-fonts-in-a-way-that-fights-fout-and-makes-lighthouse-happy/)
- [Preload, prefetch and other `<link>` tags: what they do and when to use them · PerfPerfPerf](https://3perf.com/blog/link-rels/)
- [The Simplest Way to Load CSS Asynchronously | Filament Group, Inc.](https://www.filamentgroup.com/lab/load-css-simpler/)

Following is the code I adapted for [hugo-theme-diary](https://github.com/loikein/hugo-theme-diary/blob/main/layouts/partials/head.html#L118-L129):

```html
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link rel="preload" as="style"
      href="https://fonts.googleapis.com/css?family=Lora|Noto+Serif+SC|Material+Icons&display=swap" />
<link rel="stylesheet"
      href="https://fonts.googleapis.com/css?family=Lora|Noto+Serif+SC|Material+Icons&display=swap"
      media="print" onload="this.media='all'" />
<noscript>
<link rel="stylesheet"
      href="https://fonts.googleapis.com/css?family=Lora|Noto+Serif+SC|Material+Icons&display=swap" />
</noscript>
```

#### Async \(v2\)

Not tested:

```html
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link rel="preload" as="style"
      href="https://fonts.googleapis.com/css2?family=Lora&family=Noto+Serif+SC&family=Material+Icons&display=swap" />
<link rel="stylesheet"
      href="https://fonts.googleapis.com/css2?family=Lora&family=Noto+Serif+SC&family=Material+Icons&display=swap"
      media="print" onload="this.media='all'" />
<noscript>
<link rel="stylesheet"
      href="https://fonts.googleapis.com/css2?family=Lora&family=Noto+Serif+SC&family=Material+Icons&display=swap" />
</noscript>
```

#### Weights \(v1\)

Doc: [Get Started with the Google Fonts API | Google for Developers](https://developers.google.com/fonts/docs/getting_started)

Ref: [html - How to use italic google fonts? - Stack Overflow](https://stackoverflow.com/a/28933352)

```text
http://fonts.googleapis.com/css
    ?family=Lora:400,400italic,700,700italic  # both normal and italic, regular & bold
    |Noto+Serif+SC:400,700                    # only normal, regular & bold
    &display=swap
```

#### Weights \(v2\)

Doc:

> Without style specifications, the API provides the [default style](https://developers.google.com/fonts/docs/css2#default_style) of the requested family.
> 
> > When a request doesn’t specify a position or range for an axis, the default position will be used. The default position of the italic axis is 0 (normal) and the default for the weight axis is 400 (regular).
> 
> ~ [CSS API update | Google Fonts | Google for Developers](https://developers.google.com/fonts/docs/css2#individual_styles_such_as_weight)

Ref: [Getting Variable Fonts from Google Fonts - Launch 2 Success](https://www.launch2success.com/guide/getting-google-font-variable-files/)

Getting italic variants:

```text
https://fonts.googleapis.com/css2
    ?family=Lora
        :ital,
        wght@1,400;1,700              # only italic, regular & bold
            @0,400;0,700;1,400;1,700  # both normal and italic, regular & bold
    &family=Noto+Serif+SC
        :wght@400;700                 # only normal, regular & bold
    &text=...
    &display=swap
```

#### Optimising \(v1 \& v2\)

> \[C\]onsider specifying a `text=` value in your font request URL. This allows Google Fonts to return a font file that's optimized for your request. In some cases, this can reduce the size of the font file by up to 90%.
> 
> ~ [CSS API update | Google Fonts | Google for Developers](https://developers.google.com/fonts/docs/css2#optimizing_your_font_requests)

> `subset` ≠ `text`! In Google Fonts, `subset` is for script types. It will most likely not reduce the font size to be downloaded.
{.book-hint .warning}


#### Aside: Google Fonts via `@font-face`

- [css - @font-face with Google font - Stack Overflow](https://stackoverflow.com/a/21465708)
- [majodev/google-webfonts-helper: A Hassle-Free Way to Self-Host Google Fonts. Get eot, ttf, svg, woff and woff2 files + CSS snippets](https://github.com/majodev/google-webfonts-helper)


### Subsetting

- [unicode - Subset Font By Specific Glyphs - Stack Overflow](https://stackoverflow.com/a/16674304)
- [css - How to subset Basic Latin (128 glyphs) with the Unicode range descriptor - Stack Overflow](https://stackoverflow.com/a/73269305)
- [Creating font subsets | Dev Diary](https://markoskon.com/creating-font-subsets/)
- [Font Subsetter](https://everythingfonts.com/subsetter)


## Methodologies

### Atomic CSS


### BEM

Refs:

- [CSS / Methodology / BEM](https://en.bem.info/methodology/css/)


## Queries

Refs:

- [CSS Style Queries - Ahmad Shadeed](https://ishadeed.com/article/css-container-style-queries/)


## Snippets

### Descriptive list in grid

```css
dl {
  display: grid;
  gap: 0.5rem 1rem;
  align-items: end;
}

dl dt {
  margin-top: 0;
  grid-column: 1;
}

dl dd {
  margin-bottom: 0;
  margin-left: 1rem;
}

@media screen and (min-width: 900px) {
  dl {
    grid-template-columns: fit-content(50%) auto;
  }

  dl dd {
    grid-column: 2;
    margin-left: 0;
  }
}
```

### Responsive iframe

#### New version (`aspect-ratio`)

```css
.video-container {
  width: 100%; /* this is not the actual width */
}

.video {
  width: 95%; /* this is the actual width */
}

.video--16x9{ aspect-ratio: 16/9; }
.video--4x3{ aspect-ratio: 4/3; }
```

Usage:

```html
<div class="video-container">
  <iframe
  class="video video--4x3"
  src="https://www.youtube-nocookie.com/embed/<video_id>?cc_load_policy=1&cc=1" allowfullscreen title="YouTube video" frameborder="0" sandbox="allow-same-origin allow-scripts" loading="lazy"></iframe>
</div>
```

#### Old version (`padding-bottom`)

Ref: [Responsive iframes — The Right Way (CSS Only)! | Ben Marshall](https://www.benmarshall.me/responsive-iframes/)

```css
.video-container{
  position: relative;
  height: 0;
}
    
.video-container--4x3{ padding-bottom: 75%; }
.video-container--16x9{ padding-bottom: 56.25%; }

.video-container iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
```

Usage:

```html
<div class="video-container video-container--4x3">
  <iframe src="https://www.youtube-nocookie.com/embed/<video_id>?cc_load_policy=1&cc=1" allowfullscreen title="YouTube video" frameborder="0" sandbox="allow-same-origin allow-scripts" loading="lazy"></iframe>
</div>
```

### Random shadow animation

…that I somehow made for something.

```css
.shadow {
  box-shadow: 0 .5rem 0 rgba(0,0,0,.15);
  transition: transform 0.2s, box-shadow 0.2s;
}

.shadow:hover {
  box-shadow: 0 0.7rem 0 rgba(0,0,0,.2);
  transform: translateY(-0.2rem);
  transition: transform 0.2s, box-shadow 0.2s;
}
```

### Skip-to-main button

Credit: [Hidden content for better a11y | Go Make Things](https://gomakethings.com/hidden-content-for-better-a11y/#hiding-the-link)

CSS:

```css
.screen-reader {
  border: 0;
  clip: rect(0 0 0 0);
  height: 1px;
  margin: -1px;
  overflow: hidden;
  padding: 0;
  position: absolute;
  white-space: nowrap;
  width: 1px;
}

.screen-reader-focusable:active,
.screen-reader-focusable:focus {
  display: block;       /* added */
  text-align: center;   /* added */
  clip: auto;
  height: auto;
  margin: 0;
  overflow: visible;
  position: static;
  white-space: normal;
  width: auto;
}
```

Usage:

```html
<body>
  <a class="screen-reader screen-reader-focusable" href="#main">Skip to the main content</a>
  <nav>Navigation elements...</nav>
  <main id="main">The main content</main>
  ...
</body>
```

### SVG words watermark background

Ref: [Watermark text repeated diagonally css/html - Stack Overflow](https://stackoverflow.com/a/57113720)

```css
body {
  background-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' version='1.1' height='350' width='350'><text transform='translate(50, 300) rotate(-45)' fill='WhiteSmoke' font-size='100' font-weight='bold'>DRAFT</text></svg>");
}
```

SVG code: \(see [EPUB editing #Image sizing](/programming/web/epub-editing#image-sizing) for a longer expedition of what properties should be what values \& with or without units\)

```svg
<svg xmlns='http://www.w3.org/2000/svg' version='1.1' height='350' width='350'>
  <text transform='translate(50, 300) rotate(-45)' fill='WhiteSmoke' font-size='100' font-weight='bold'>DRAFT</text>
</svg>
```


## Readings

- [The Guide To Responsive Design In 2023 and Beyond - Ahmad Shadeed](https://ishadeed.com/article/responsive-design/)
- [A Complete Guide to CSS Concepts and Fundamentals | Tania Rascia](https://www.taniarascia.com/overview-of-css-concepts/)
- [Modern CSS Solutions](https://moderncss.dev/)
- [CSS debt](https://mtm.dev/css-debt)
- [A Complete Guide to CSS Grid | CSS-Tricks - CSS-Tricks](https://css-tricks.com/snippets/css/complete-guide-grid/)
- [A Complete Guide to Flexbox | CSS-Tricks - CSS-Tricks](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)


## Tools/Generators

### Colours

- [OddContrast](https://www.oddcontrast.com/ \(any input, any sliders, any output\)
- [Colorable](https://colorable.jxnblk.com/ffffff/000000) \(HEX input, HSL sliders\)
  + Very similar: [Colour Contrast Checker](https://colourcontrast.cc/ffffff/000000)
- [Color.review - Colors that look and work great for everyone](https://color.review/) \(big colour picker with iso-contrast contour lines\)
- [EightShapes Contrast Grid](https://contrast-grid.eightshapes.com/) \(cross-check many colours all at once\)
- [WhoCanUse](https://www.whocanuse.com/) \(visual impairment simulations\)

### Shadow

- [CSS Shadow Palette Generator](https://www.joshwcomeau.com/shadow-palette/)

### Pattern

- [Free SVG generators, color tools & web design tools](https://fffuel.co/)
  + [SVG Generators — Smashing Magazine](https://www.smashingmagazine.com/2021/03/svg-generators/#svg-background-generators)
- [CSS Polka Dot Generator](https://screenspan.net/polka/)

## Entertainment

- [How to Make iOS Text Messages on AO3 - Chapter 1 - CodenameCarrot, La_Temperanza - No Fandom [Archive of Our Own]](https://archiveofourown.org/works/6434845/chapters/14729722)
- [CSS Grid: Excel Spreadsheet](https://codepen.io/oliviale/pen/rPjgmB)
