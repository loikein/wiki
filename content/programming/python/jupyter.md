---
weight: 500
title: "Jupyter Notebook/Lab"
---

## Basics

Convert to HTML:

```bash
$ jupyter nbconvert --execute --to html my_notebook.ipynb
```

## Custom CSS for Lab

For usage see: [Browser extension #Customise the web](/computer/internet/browser-extension/#customise-the-web)

Range: URLs starting with: `http://localhost:8888/lab`

```css
/* my file names are too long */
/* whole file name */
.jp-DirListing-item {
  padding: 4px;
}

/* kernel running indicator */
.jp-DirListing-item.jp-mod-running .jp-DirListing-itemIcon::before {
  left: -5px;
}

/* file icon */
.jp-DirListing-itemIcon {
  flex: 0 0 16px;
}

/* file name text */
.jp-DirListing-itemText {
  text-overflow: clip;
}

/* date modified */
.jp-DirListing-itemModified {
  flex: 0 0 95px;
}
```

## Settings

Ref: [jupyterlab/packages/codemirror/src/extension.ts at main · jupyterlab/jupyterlab](https://github.com/jupyterlab/jupyterlab/blob/main/packages/codemirror/src/extension.ts )


## Useful Notebook Extensions

TBA
