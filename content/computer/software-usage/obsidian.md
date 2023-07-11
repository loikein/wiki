---
weight: 400
title: "Obsidian"
---
{{< hint warning >}}
I have not touched Obsidian for over a year and am still figuring out the new features \& mobile versions.
{{< /hint >}}

## Plugins

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


## Working with multiple vaults

Set a different accent colour for each vault for a more obvious visual reminder.
