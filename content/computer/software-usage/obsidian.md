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

### cm-show-whitespace-obsidian

Repo: [deathau/cm-show-whitespace-obsidian](https://github.com/deathau/cm-show-whitespace-obsidian)

{{< details "Reference: Core styles of this plugin" >}}
```css
body.plugin-cm-show-whitespace .cm-whitespace::before,
body.plugin-cm-show-whitespace .cm-tab::before,
body.plugin-cm-show-whitespace .CodeMirror-code > div > pre > span > :last-child:after,
body.plugin-cm-show-whitespace .CodeMirror-line > span > :last-child::after,
body.plugin-cm-show-whitespace [class*=cm-trailing-space] + [class*=cm-trailing-space]:last-child::after {
    pointer-events: none;
    color: var(--text-faint);
    font-weight: normal;
    opacity: 0.5;
}

body.plugin-cm-show-whitespace {
    --spaceChar: "·";
    --trailingSpaceChar: "·";
    --singleSpaceChar: var(--spaceChar);
    --tabChar: "→";
    --newlineChar: "¬";
    --strictLineBreakChar: var(--newlineChar);
}
```
{{< /details >}}

Because this plugin has been unmaintained for a while, a patch is needed to make everything look consistent. Add a CSS file with the following contents:

```css
body.plugin-cm-show-whitespace [class*=cm-trailing-space]::after,
body.plugin-cm-show-whitespace [class*=cm-trailing-space]::before {
    color: var(--text-faint);
}
```

### control-characters

Repo: [joethei/obsidian-control-characters](https://github.com/joethei/obsidian-control-characters)

When I was looking for an alternative of [cm-show-whitespace-obsidian](#cm-show-whitespace-obsidian), I found this plugin which also integrates with [mgmeyers/obsidian-style-settings](https://github.com/mgmeyers/obsidian-style-settings) to make customising possible without fiddling with CSS files. However, I did not like the default SVGs, and could not bother with finding new SVGs right now, so I am still using the old plugin.

### hover-editor

Repo: [nothingislost/obsidian-hover-editor](https://github.com/nothingislost/obsidian-hover-editor)

Need to turn on the core Page Preview plugin first, or force reload.

Together with `![[]]` embed, and setting hotkeys {{< kbd `option` `↑` >}} and {{< kbd `option` `↓` >}} for swap lines \(credit: [@seviche@kongwoo.icu](https://kongwoo.icu/users/seviche)\) makes an ok block-editing environment[^ulysses].

[^ulysses]: Yes, I am still missing the Ulysses block editing feature.

### stille

Repo: [michaellee/stille](https://github.com/michaellee/stille)

If after tweaks of other plugins, the opaque effect disappears, just go to setting and change the opacity number a bit and it will come back.


## Plugins \(for aggressive note-taking\)

TBE.


## Themes

### obsidian-ia-writer

Repo: [mrowa44/obsidian-ia-writer](https://github.com/mrowa44/obsidian-ia-writer)

1. The recommended accent colour \(<div title="#18BEEC" style="height: 30px; background-color: #18BEEC; display: inline-block; border-style: solid; border-color: black; color:black; padding-left: 5px; padding-right: 5px;">#18BEEC</div>\) is a bit too light for me, and I used <div title="#4480EF" style="height: 30px; background-color: #4480EF; display: inline-block; border-style: solid; border-color: black; color:white; padding-left: 5px; padding-right: 5px;">#4480EF</div> which has a similar saturation to the default colour.
1. The recommended [artisticat1/focus-active-sentence](https://github.com/artisticat1/focus-active-sentence) plugin blinks when scrolling the page, which I found distracting. Instead, I tried [michaellee/stille](https://github.com/michaellee/stille) with opacity 0.3, which turned out great.
1. Unfortunately, the very appealing [artisticat1/nl-syntax-highlighting](https://github.com/artisticat1/nl-syntax-highlighting) only supports English, which is not my primary writing language in Obsidian.


## Things to keep an eye on

For writing:

- [Plugins for Writers - Obsidian Hub - Obsidian Publish](https://publish.obsidian.md/hub/02+-+Community+Expansions/02.01+Plugins+by+Category/Plugins+for+Writers)
- [Plugins for Editing Notes - Obsidian Hub - Obsidian Publish](https://publish.obsidian.md/hub/02+-+Community+Expansions/02.01+Plugins+by+Category/Plugins+for+Editing+Notes)
- [Chinese Language Plugins - Obsidian Hub - Obsidian Publish](https://publish.obsidian.md/hub/02+-+Community+Expansions/02.01+Plugins+by+Category/Chinese+Language+Plugins)
- [Japanese Language Plugins - Obsidian Hub - Obsidian Publish](https://publish.obsidian.md/hub/02+-+Community+Expansions/02.01+Plugins+by+Category/Japanese+Language+Plugins)
- [Dictionary and Spellchecking Plugins - Obsidian Hub - Obsidian Publish](https://publish.obsidian.md/hub/02+-+Community+Expansions/02.01+Plugins+by+Category/Dictionary+and+Spellchecking+Plugins)
- [Plugins Designed for Mobile - Obsidian Hub - Obsidian Publish](https://publish.obsidian.md/hub/02+-+Community+Expansions/02.01+Plugins+by+Category/Plugins+Designed+for+Mobile)

For note-taking:

- TBE
