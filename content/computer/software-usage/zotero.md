---
weight: 400
title: "Zotero"
---

## Useful tricks

### See all collections an item is in

> [How can I see what collections my item is in? [Zotero Documentation]](https://www.zotero.org/support/kb/collections_containing_an_item)
> 
> To see all the collections an item is in, select the item and then hold down the {{< kbd "Option" >}} key (macOS), {{< kbd "Control" >}} key (Windows), or {{< kbd "Alt" >}} key (Linux). This will highlight all collections that contain the selected item.

### Use outside PDF viewer on iOS

> [Using an External PDF Reader with iOS App - Zotero Forums](https://forums.zotero.org/discussion/comment/428370/#Comment_428370)
> 
> 1. Open the PDF on Zotero and share to GoodNotes (include annotations if you already have some)
> 2. Read and highlight/annotate the PDF in Goodnotes
> 3. Once you are done, share from GoodNotes to Zotero (include annotations obviously)
> 4. The PDF will appear as a separate entry in the library. Drag and drop it onto the original entry, and it will be moved there. Tap on 'i' to check that there should now be two PDFs for the same entry
> 5. Delete the old PDF from that entry by long press and 'Move to Trash'


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
