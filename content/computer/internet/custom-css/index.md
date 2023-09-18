---
weight: 200
title: "Custom CSS"
---

For usage see: [Browser extension #Customise the web](/computer/internet/browser-extension/#customise-the-web)

Some of the bugs may have been caused by my browser settings. Adopt after careful inspection.

## Universal

Range: Everything

```css
s, strike, del {
    opacity: 60%;
}
```

## AO3

> **Applying multiple custom CSS for logged-in users**:
>
> First, go to Dashboard ▸ Skins ▸ My Site Skins, create at least one skin for dark theme \(because `prefers-color-scheme` will be applied to the whole skin\) and one skin for other general styles.
>
> Then, create a third skin with no CSS code, go to Advanced ▸ Parent Skins ▸ Add parent skin, add all the sub-skins you want to apply.
>
> Use this final skin as your site skin. Now you have everything. Every time you want to add other CSS **on top of** your current configuration, make sub skins then add them as parents to this big skin.
{.book-hint .info}

Range: URLs on the domain: `archiveofourown.org`

```css
/* limit line length */
#main {
    max-width: 80ch;
}
```

{{< details "Dark theme" >}}
This is AO3's [official dark theme](https://archiveofourown.org/skins/929). If you already have a skin of it, please ignore.

{{< highlight-file file="reversi-skin-by-ao3.css" lang="css" >}}
{{< /details >}}

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
