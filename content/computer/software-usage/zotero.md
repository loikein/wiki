---
weight: 400
title: "Zotero"
---

# Zotero

## Useful commands

> [How can I see what collections my item is in? [Zotero Documentation]](https://www.zotero.org/support/kb/collections_containing_an_item)
> 
> To see all the collections an item is in, select the item and then hold down the {{< kbd "Option" >}} key (macOS), {{< kbd "Control" >}} key (Windows), or {{< kbd "Alt" >}} key (Linux). This will highlight all collections that contain the selected item. 

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

<!-- 
### ZotFile

Repository: [jlegewie/zotfile: Zotero plugin to manage your attachments](https://github.com/jlegewie/zotfile)
 -->

### QuickLook

Repository: [mronkko/ZoteroQuickLook: Implements QuickLook in Zotero](https://github.com/mronkko/ZoteroQuickLook)

### OCR

Repository: [UB-Mannheim/zotero-ocr: Zotero Plugin for OCR](https://github.com/UB-Mannheim/zotero-ocr)

### Date Grabber

Repository: [retorquere/zotero-date-from-last-modified](https://github.com/retorquere/zotero-date-from-last-modified/tree/master)

### scite

Repository: [scitedotai/scite-zotero-plugin: scite zotero plugin](https://github.com/scitedotai/scite-zotero-plugin)

## Use Sci-Hub as Default PDF Finder

List of online Sci-Hub URLs: [List of sci hub and libgen active urls - Verts-Luisants](https://vertsluisants.fr/index.php?article4/)

Open Preferences > Advanced > Config Editor, search for `extensions.zotero.findPDFs.resolvers`, paste the following into Value: \([credit](https://zhuanlan.zhihu.com/p/112141757)\)

```json
{
	"name":"Sci-Hub",
	"method":"GET",
	"url":"https://scihub.wikicn.top/{doi}",
	"mode":"html",
	"selector":"#pdf",
	"attribute":"src",
	"automatic":true
}
```

## Add Custom Lookup Engines

References:

- [locate \[Zotero Documentation\]](https://www.zotero.org/support/locate)
- [Adding search engines \- Zotero Forums](https://forums.zotero.org/discussion/37129/adding-search-engines)
- Some other engines: [zotero\-tools/engines.json](https://github.com/bwiernik/zotero-tools/blob/master/engines.json)

1. Open `~/Zotero/locate/engines.json`.
2. Before the closing `]`, add the following code:
3. Download the icon, rename and place it at `~/Zotero/locate/sementic_scholar.png`.
4. Restart Zotero.

```json
	,
	{
		"_name": "Semantic Scholar Search",
		"_alias": "Semantic Scholar",
		"_description": "Semantic Scholar Search",
		"_icon": "file:///Users/loikein/Zotero/locate/sementic_scholar.png",
		"_urlTemplate": "https://www.semanticscholar.org/search?year%5B0%5D={z:year?}&year%5B1%5D={z:year?}&q={z:title}&sort=relevance",
		"_urlParams": [],
		"_urlNamespaces": {
			"z": "http://www.zotero.org/namespaces/openSearch#",
			"": "http://a9.com/-/spec/opensearch/1.1/"
		},
		"_iconSourceURI": "https://www.semanticscholar.org/img/favicon.png"
	}
```
