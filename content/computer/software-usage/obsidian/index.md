---
weight: 400
title: "Obsidian"
---

> I have not touched Obsidian for over a year and am still figuring out the new features \& the mobile apps.
{.book-hint .warning}

## Admin

### Sync between devices

Do not use iCloud WITH git. Pick one.


### Working with multiple vaults

Set a different accent colour for each vault for a more obvious visual reminder.



## Plugins \(for peaceful writing\)

### Show Whitespace

Repo: [deathau/cm-show-whitespace-obsidian](https://github.com/deathau/cm-show-whitespace-obsidian)

{{< details "Reference: Core styles of this plugin, obtained from inspection" >}}
Source: [deathau/cm-show-whitespace-obsidian/styles.scss](https://github.com/deathau/cm-show-whitespace-obsidian/blob/main/styles.scss)

{{< highlight-file file="cm-show-whitespace-core.css" lang="css" >}}
{{< /details >}}

Because this plugin has been unmaintained for a while, a patch is needed to make everything look consistent. Add a CSS file with the following contents: \(the `<br>` style came from [here](https://stackoverflow.com/a/64912130)\)

```css
body.plugin-cm-show-whitespace [class*=cm-trailing-space]::after,
body.plugin-cm-show-whitespace [class*=cm-trailing-space]::before {
  /* sometimes one of these doesn't work depending on the theme: */
  /* color: var(--text-faint); */
  color: var(--text-muted);
}
.markdown-source-view br {
  content: "&nbsp;";
  display: block;
}
.markdown-source-view br::after {
  content: var(--newlineChar);
  white-space: pre;
  pointer-events: none;
  color: var(--text-muted);
  font-weight: normal;
  opacity: 0.5;
}
```

#### Control Characters

Repo: [joethei/obsidian-control-characters](https://github.com/joethei/obsidian-control-characters)

When I was looking for an alternative of [cm-show-whitespace-obsidian](#cm-show-whitespace-obsidian), I found this plugin which also integrates with [mgmeyers/obsidian-style-settings](https://github.com/mgmeyers/obsidian-style-settings) to make customising possible without fiddling with CSS files. However, I did not like the default SVGs, and could not bother with finding new SVGs right now, so I am still using the old plugin.

### Hider

Repo: [kepano/obsidian-hider](https://github.com/kepano/obsidian-hider)

Hide ribbon, vault name, file explorer icons when in writing mode.

### Hover Editor

Repo: [nothingislost/obsidian-hover-editor](https://github.com/nothingislost/obsidian-hover-editor)

Need to turn on the core Page Preview plugin first, or force reload.

Together with `![[]]` embed, and setting hotkeys {{< kbd `option` `↑` >}} and {{< kbd `option` `↓` >}} for swap lines \(credit: [@seviche@kongwoo.icu](https://kongwoo.icu/users/seviche)\) makes an ok block-editing environment[^ulysses].

[^ulysses]: Yes, I am still missing the Ulysses block editing feature.


### Quiet Outline

Repo: [guopenghui/obsidian-quiet-outline](https://github.com/guopenghui/obsidian-quiet-outline)

Use Command palette ▸ Quiet Outline: Quiet Outline to activate.

Turning on dragging titles to rearrange document for a pseudo block editing experience.

Some styles I wrote for more obvious current entry highlighting:

```css
/* **** all entries **** */
.n-tree .n-tree-node {
  --n-node-text-color: var(--nav-item-color);
  transition: none;
  font-size: var(--nav-item-size);
  border-radius: var(--radius-s);
}

.quiet-outline .n-tree-node .n-tree-node-content {
  margin-bottom: var(--size-2-1);
  padding: var(--nav-item-padding);
  padding-left: 0;
  line-height: var(--line-height-tight);
}

/* **** cursor-focused entries **** */
.n-tree.n-tree--block-line .n-tree-node:not(.n-tree-node--disabled).n-tree-node--selected {
  /* accent highlight */
  background-color: var(--interactive-accent) !important;
  /* muted highlight */
  /* background-color: var(--nav-item-background-hover) !important; */
}
.n-tree .n-tree-node--selected .n-tree-node-content .n-tree-node-content__text {
  color: var(--text-on-accent) !important;
  font-weight: normal !important;
}

/* **** scrolled-to entries **** */
.n-tree .n-tree-node.located {
  background-color: var(--nav-item-background-hover) !important;

  font-weight: normal !important;
}

/* **** hovered entries **** */
.quiet-outline .n-tree.n-tree--block-line .n-tree-node:not(.n-tree-node--disabled):hover {
  background-color: var(--nav-item-background-hover);
}

/* **** expand switcher **** */
.n-tree .n-tree-node-switcher {
  height: unset;
}
```

### Stille

Repo: [michaellee/stille](https://github.com/michaellee/stille)

Click the moon icon in the [Ribbon](https://help.obsidian.md/User+interface/Workspace/Ribbon), or use Command palette ▸ Stille: Toggle Stille to activate.


## Plugins \(for aggressive note-taking\)

TBE.


## Themes

### iA Writer

Repo: [mrowa44/obsidian-ia-writer](https://github.com/mrowa44/obsidian-ia-writer)

<!-- The recommended accent colour \(<span title="#18BEEC" style="height: 30px; background-color: #18BEEC; display: inline-block; border-style: solid; border-color: black; color:black; padding-left: 5px; padding-right: 5px;">#18BEEC</span>\) is a bit too light for me, and I used <span title="#4480EF" style="height: 30px; background-color: #4480EF; display: inline-block; border-style: solid; border-color: black; color:white; padding-left: 5px; padding-right: 5px;">#4480EF</span> which has a similar saturation to the default purple colour. -->

The recommended [artisticat1/focus-active-sentence](https://github.com/artisticat1/focus-active-sentence) plugin blinks when scrolling the page, which I found distracting. Instead, I tried [michaellee/stille](https://github.com/michaellee/stille) which turned out to be great.

Unfortunately, the very appealing [artisticat1/nl-syntax-highlighting](https://github.com/artisticat1/nl-syntax-highlighting) only supports English, which is not my primary writing language in Obsidian.

The file tree is very buggy on my setup.


### iB Writer

Repo: [whereiswhere/iB-Writer](https://github.com/whereiswhere/iB-Writer)

Less buggy than iA Writer, but does not respect the accent colour setting.

Some tiny fixes to this theme that I wrote:

```css
.markdown-source-view {
  font-size: unset;
}

body:not(.is-grabbing) .nav-file-title.is-active:hover,
body:not(.is-grabbing) .nav-folder-title.is-active:hover,
.nav-file-title.is-active, .nav-folder-title.is-active {
  color: var(--text-on-accent);
}

.cm-s-obsidian span.cm-hmd-internal-link:hover {
  color: var(--indicator-color, var(--interactive-accent));
}
```

### Minimal

Repo: [kepano/obsidian-minimal](https://github.com/kepano/obsidian-minimal)

Changed a lot of CSS classes \(maybe for good but very confusing when writing snippets\). It did not made a huge difference to me compared to default theme with [Hider](#hider), so in the end I went back to that.

Some styles I wrote to make the right sidebar to have the same background colour as the left sidebar:

```css
.workspace-split.mod-right-split .workspace-tabs {
    --tab-container-background: var(--bg2) !important;
    --background-secondary: var(--bg2) !important;
    --titlebar-background-focused: var(--bg2) !important;
}

.sidebar-toggle-button.mod-right {
    background-color: var(--bg2) !important;
}
```


## General CSS nippets

> - Style for `text-decoration` will not apply in selection layer.
> - `::selection` does not work for some reason.
{.book-hint .info}

### Thicker cursor \(kind of\)

Nothing really worked. I also tried [Ninja cursor](https://github.com/vrtmrz/ninja-cursor), no luck with Obsidian 1.3.7.

{{< details "Reference: Core styles of the default cursors, obtained from inspection" >}}
The characters are not typos.
{{< highlight-file file="default-cursor.css" lang="css" >}}
{{< /details >}}

There are two types of cursors, `.cm-cursor` \(end-border of selection\) and `.cm-dropCursor` \(caret when user is typing\). The following style only works on the former, using accent colour from iB theme, with default accent as fallback.

```css
/* disable animation for cm-cursor */
.ͼ1.cm-focused>.cm-scroller>.cm-cursorLayer {
  animation: none !important;
}

/* colour and width for cm-cursor */
/* better than border-left method for more consistent sizes */
/* adding .ͼ1 .cm-dropCursor here makes no difference */
.ͼ1 .cm-cursor {
  visibility: visible !important;
  display: block;
  position: absolute;
  border: none;
  white-space: pre;
  outline: 1px solid var(--indicator-color, var(--interactive-accent));
  color: transparent !important;
  margin-left: 0.5px;
}

/* colour for cm-dropCursor */
.markdown-source-view.mod-cm6 .cm-content {
  caret-color: var(--indicator-color, var(--interactive-accent));
}
```

### iA Writer CSS for default theme

First 29 lines of [mrowa44/obsidian-ia-writer/theme.css](https://github.com/mrowa44/obsidian-ia-writer/blob/main/theme.css) \(Base64 encoded iA Writer Duo font, too large to include here\), plus:

{{< highlight-file file=`theme-default-ia-trim.css` lang=`css` >}}

### Fade out sidebars when not in use

```css
.mod-left-split:not(:hover),
.mod-right-split:not(:hover) {
  opacity: 0.3;
}
```

## Things to keep an eye on

For writing:

- [Plugins for Writers - Obsidian Hub - Obsidian Publish](https://publish.obsidian.md/hub/02+-+Community+Expansions/02.01+Plugins+by+Category/Plugins+for+Writers)
- [Plugins for Editing Notes - Obsidian Hub - Obsidian Publish](https://publish.obsidian.md/hub/02+-+Community+Expansions/02.01+Plugins+by+Category/Plugins+for+Editing+Notes)
- [Chinese Language Plugins - Obsidian Hub - Obsidian Publish](https://publish.obsidian.md/hub/02+-+Community+Expansions/02.01+Plugins+by+Category/Chinese+Language+Plugins)
- [Japanese Language Plugins - Obsidian Hub - Obsidian Publish](https://publish.obsidian.md/hub/02+-+Community+Expansions/02.01+Plugins+by+Category/Japanese+Language+Plugins)
- [Dictionary and Spellchecking Plugins - Obsidian Hub - Obsidian Publish](https://publish.obsidian.md/hub/02+-+Community+Expansions/02.01+Plugins+by+Category/Dictionary+and+Spellchecking+Plugins)
- [Plugins Designed for Mobile - Obsidian Hub - Obsidian Publish](https://publish.obsidian.md/hub/02+-+Community+Expansions/02.01+Plugins+by+Category/Plugins+Designed+for+Mobile)
- [Outdented marks / Hanging punctuation - Help - Obsidian Forum](https://forum.obsidian.md/t/outdented-marks-hanging-punctuation/34527)

For note-taking:

- [Obsidian Web Clipper — Steph Ango](https://stephanango.com/obsidian-web-clipper)
