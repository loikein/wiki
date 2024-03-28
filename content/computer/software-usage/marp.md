---
weight: 400
title: "Marp"
---
Write slides in Markdown and CSS.

Links:

- [Marp: Markdown Presentation Ecosystem](https://marp.app/)
- [Marpit Markdown](https://marpit.marp.app/markdown)
- [marp-team/marp-core: The core of Marp converter](https://github.com/marp-team/marp-core#features)
- [marp-team/marp-vscode: Marp for VS Code: Create slide deck written in Marp Markdown on VS Code](https://github.com/marp-team/marp-vscode?tab=readme-ov-file#usage) \(Integrates marp-cli, no need to install on machine.\)


## Example slide deck

````markdown
---
marp: true
size: 4:3
---
<style>
table {
    font-size: 0.7rem
}
</style>

# Meeting

---

## Topic 1

- ...
- ...
````

## Debugging VSC/Codium

### Export as PDF requires Chrome or Edge installation

First export to HTML, then print and save as PDF from browser (check `scale` instead of `fit to page width`).


### Only images from the same folder of slides

According to [Issue #64 of marp-team/marp-vscode](https://github.com/marp-team/marp-vscode/issues/64), this is by restriction \(design\) of VSC.
