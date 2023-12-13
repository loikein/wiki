---
weight: 400
title: "Zotero"
---
## \(Maybe\) Useful resources

- [Install Zotero - Zotero - Library Guides at UC Berkeley](https://guides.lib.berkeley.edu/zotero)


## Useful tricks

### Export annotations from PDF to notes

> [kb:zotfile_extract_annotations [Zotero Documentation]](https://www.zotero.org/support/kb/zotfile_extract_annotations)
> 
> {{< menu `Right-click on article/PDF file` `Add Note from Annotations` >}}

Downside: It does not include text annotations.

### Export notes to Markdown/HTML file

{{< menu `Right-click on note` `Export Notes…` `Select format` `OK` >}}, then you will be prompted to select path and confirm.

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

{{< details "Plugins that I have tried but did not keep" >}}
- [windingwind/zotero-better-notes: Everything about note management. All in Zotero.](https://github.com/windingwind/zotero-better-notes#note-export)
- [jlegewie/zotfile: Zotero plugin to manage your attachments: automatically rename, move, and attach PDFs (or other files) to Zotero items, sync PDFs from your Zotero library to your (mobile) PDF reader (e.g. an iPad, Android tablet, etc.), and extract PDF annotations.](https://github.com/jlegewie/zotfile/tree/master)
- [argenos/zotero-mdnotes: A Zotero plugin to export item metadata and notes as markdown files](https://github.com/argenos/zotero-mdnotes)
{{< /details >}}

{{< details "Plugins that I would like to try later" >}}
- [wshanks/Zutilo: Zotero plugin providing some additional editing features](https://github.com/wshanks/Zutilo)
{{< /details >}}


### Better BibTeX

Documentation: [Better BibTeX for Zotero](https://retorque.re/zotero-better-bibtex/)

My configuration:

```text
Citation key format:         [zotero:clean]
Fields to omit from export:  file, note, keywords, abstract
```

### Date Grabber

Repository: [retorquere/zotero-date-from-last-modified](https://github.com/retorquere/zotero-date-from-last-modified/tree/master)


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

After applying fixes from the Issues \([1](https://github.com/mronkko/ZoteroQuickLook/issues/44#issuecomment-1079053758), [2](https://github.com/mronkko/ZoteroQuickLook/issues/44#issuecomment-1079624343)\), it works with Zotero 6 well.

### OCR

Repository: [UB-Mannheim/zotero-ocr: Zotero Plugin for OCR](https://github.com/UB-Mannheim/zotero-ocr)


### scite

Repository: [scitedotai/scite-zotero-plugin: scite zotero plugin](https://github.com/scitedotai/scite-zotero-plugin)

### Special tags column

Repo: [whacked/zotero-special-tags-column: Plugin to add a "Special Tags" column into Zotero where you can display specific, pre-defined tags](https://github.com/whacked/zotero-special-tags-column)

Add custom tag display mappings. I made a star-rating \(well, more like moon-rating\) system with it.

My configuration:

```text
{"5-star":"🌕🌕🌕🌕🌕","4-star":"🌕🌕🌕🌕🌑","3-star":"🌕🌕🌕🌑🌑","2-star":"🌕🌕🌑🌑🌑","1-star":"🌕🌑🌑🌑🌑","0-star":"🌑🌑🌑🌑🌑"}
```

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
