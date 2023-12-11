---
weight: 200
title: "Custom CSS"
---

For usage see: [Browser extension #Customise the web](/computer/internet/browser-extension/#customise-the-web)

Some of the bugs may have been caused by my browser settings. Adopt after careful inspection.

## Universal

Range: Everything

```css
/* opacify del tags */
s, strike, del {
    opacity: 60%;
}
```

## AO3

Range for all styles here: URLs on the domain: `archiveofourown.org`

> **Applying multiple custom CSS for logged-in users**:
>
> First, go to {{< menu `Dashboard` `Skins` `My Site Skins` >}}, create at least one skin for dark theme \(because `prefers-color-scheme` will be applied to the whole skin\) and one skin for other general styles.
>
> Then, create a third skin \(the big-skin\) with no CSS code, go to {{< menu `Advanced` `Parent Skins` `Add parent skin` >}}, add all the sub-skins you want to apply.
>
> Use this big-skin as your site skin. Now you have everything. Every time you want to add other CSS <u>on top of</u> your current configuration, <u>make sub-skins then add them as parents</u> to the big-skin. Every time you update any sub-skin, the big-skin will automatically update itself.
{.book-hint .info}

### Dark theme

{{< details `This is AO3's [official dark theme](https://archiveofourown.org/skins/929). If you already have a skin of it, or have your own dark theme browser plug-in, please ignore.` >}}
{{< highlight-file file="reversi-skin-by-ao3.css" lang="css" >}}
{{< /details >}}

### Readable line width

```css
/* limit line length */
#main {
    max-width: 80ch;
}
```

### Hide/highlight works with certain tags/languages/authors

Refs:

- [How to Block Tags With Site Skins (And Get Real Specific About It) - Chapter 1 - najio - No Fandom \[Archive of Our Own\]](https://archiveofourown.org/works/41589201/chapters/104315178#workskin)
- [Attribute selectors - CSS: Cascading Style Sheets | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors)

```css
/* truncate & opacify works */
/* by tag or work URL */
.blurb:has(a[href*="Some%20Character*s*Another%20Character"]),
.blurb:has(a[href*="/works/..."]) {
  opacity: 0.3;
  max-height: 200px;
  overflow: hidden;
}

.blurb > .header {
  opacity: inherit;
}

/* mark works with their languages */
.blurb:has(.language[lang*="es"])::before {
  content: "es";
  position: absolute;
  font-size: 50px;
  right: 50px;
  color: #900;
}

/* highlight works from certain users or pseuds */
/* by author url */
.blurb:has(a[href*="/users/.../pseuds/..."]) {
  background: yellow;
}
```

### \(Unsuccessful\) Adjust order of elements in work blurb

**Failed attempts** to make the stats (Language / Word count / Chapter plan) appear first, then tags, then summary.

{{< details `Flexbox version that is not compatible with AO3 site skin system.` >}}
```css
ol.work > li.blurb {
  display: flex;
  flex-direction: column;
  gap: .643em;
}

.blurb>.header, .blurb>dl, .blurb>blockquote {
  margin: 0;
}

.blurb>.landmark {
  display: none;
  visibility: collapse;
}

.blurb>.header {
  order: -2;
}

.blurb dl.stats {
  order: -1;
  text-align: left;
}
```
{{< /details >}}

{{< details `Clumsier table version that is compatible with AO3's site skin system, but not with iOS Safari.` >}}
Bonus: It voids any height-clipping CSS for the work blurbs.

Ref: [html - Switching the order of block elements with CSS - Stack Overflow](https://stackoverflow.com/a/25309319)

```css
ol.work > li.blurb {
  display: table;
}

ol.work > li.blurb >.header {
  display: table-caption;
  margin-top: .375em;
  border-top: 5px solid #ddd;
}

ol.work > li.blurb > dl.stats {
  float: none;
  display: table-header-group;
  text-align: left;
}

ol.work > li.blurb > ul.tags {
  margin-top: .643em;
}
```
{{< /details >}}

### Hide in-text illustrations

I'm sorry, authors, I don't want to see those AI-generated illustrations of my fav characters.

```css
/* hide in-text illustrations */
#workskin p img {
  display: none !important;
  visibility: collapse !important;
}
```

## GitHub

Range: URLs on the domain: `github.com`

{{< highlight-file file="github-1.css" lang="css" >}}

Range: URLs on the domain: `github.com` \(thanks to [thehale](https://github.com/refined-github/refined-github/issues/6656#issuecomment-1629464380)\)

```css
/* highlight private repos in repo list */
li.private .Label--secondary {
    border-color: var(--color-attention-muted);
    color: var(--color-attention-emphasis);
}
```

Range: URLs matching the regexp: `.*github\.com/.*/.*/pull/.*`

```css
/* hide inline annotation option when looking at PR */
.js-inline-annotations {
    display: none;
    visibility: collapse;
}
```

## Jupyter Lab

See: [Jupyter Notebook/Lab](/programming/python/jupyter/#custom-css)


## Office Online

Range: URLs on the domain: `officeapps.live.com` (particularly within iframes)

{{< highlight-file file="office-1-colour.css" lang="css" >}}

{{< highlight-file file="office-2-border.css" lang="css" >}}


## Python documentations

Range: URLs on the domain: `pandas.pydata.org`, `numpy.org`

```css
/* highlight param names */
dt strong {
  color: var(--pst-color-primary);
}
```

Range: URLs on the domain: `seaborn.pydata.org`, `matplotlib.org` \(because their primary colour is too dark\)

```css
dt strong {
  color: var(--pst-color-info);
}
```

Range: URLs on the domain: `pythonhosted.org`

```css
/* highlight param names */
ul li strong {
    color: #3fb79c;
}
```

Range: URLs on the domain: `scikit-learn.org`

```css
/* highlight param names */
dt strong {
  color: var(--primary); /* bootstrap colour */
}
```

Range: URLs on the domain: `statsmodels.org`

```css
/* highlight param names */
dt strong {
  color: var(--md-primary-fg-color);
}
dt .classifier a {
  color: unset;
}

/* unset scroll bar highlight */
.md-typeset pre > code,
.md-typeset pre > code:hover {
  scrollbar-color: unset;
}
```

Range: URLs on the domain: `mathurinm.github.io`

```css
/* celer doc */
/* highlight param names */
dt strong {
  color: var(--color-brand-content);
}
```


## Wayback Machine

Range: URLs on the domain: `web.archive.org`

```css
/* improve a11y on older sites */
:focus:not([tabindex="-1"]) {
  outline: 5px solid #CF3643;
  outline-offset: 1px;
  border: 0;
}
```
