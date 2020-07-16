# Zotero

## Useful Plug-Ins

### Better BibTeX

Documentation: [Better BibTeX for Zotero](https://retorque.re/zotero-better-bibtex/)

My configuration:

```text
Citation key format:         [zotero:clean]
Fields to omit from export:  file, note, keywords, abstract
```

### DOI Manager

Repository: [bwiernik/zotero-shortdoi: Zotero extension to retrieve and validate DOIs and shortDOIs](https://github.com/bwiernik/zotero-shortdoi)

My configuration:

```text
Get DOIs for new items:     Long DOIs
```

### QuickLook

Repository: [mronkko/ZoteroQuickLook: Implements QuickLook in Zotero](https://github.com/mronkko/ZoteroQuickLook)

### OCR

Repository: [UB-Mannheim/zotero-ocr: Zotero Plugin for OCR](https://github.com/UB-Mannheim/zotero-ocr)


## Use Sci-Hub as Default PDF Finder

Open Preferences > Advanced > Config Editor, search for `extensions.zotero.findPDFs.resolvers`, paste the following into Value: \([credit](https://zhuanlan.zhihu.com/p/112141757)\)

```json
{
    "name":"Sci-Hub",
    "method":"GET",
    "url":"https://sci-hub.tw/{doi}",
    "mode":"html",
    "selector":"#pdf",
    "attribute":"src",
    "automatic":true
}
```
