---
weight: 20
title: "PDF"
---
> Everything below is macOS-specific.
{.book-hint .info}

I decided to start to collect everything I know about PDF in one place, because it has very, very frustrating for a very, very long time.


## Export annotations

Typically, there are a number of things that you can do to a PDF file in standard PDF readers that are considered to be "annotations" instead of "edits". These are the names I shall call them by hereafter:

- Highlight: Add background colour to words and characters
- Underline: Add underline to words and characters
- Annotate: Insert text boxes with text inside
- Draw: Insert shapes or freehand drawings on pages

Very frustratingly, not every PDF reader understands the same set of annotations, and not every PDF reader can export everything that they understands.

If you have a PDF file with pre-existing annotations in them, here is how to export them as \(more or less\) portable text files.

### PDF Expert

PDF Expert is a [paid software](https://pdfexpert.com/pricing).

{{< menu `File` `Export Annotation Summary as…` >}}, then choose from {{< menu `HTML` >}}, {{< menu `Plain text` >}}, and {{< menu `Markdown` >}}.

Differences between the three versions:

|            | Context of highlights | TOC | Page number | Author and time |
|:-----------|:---------------------:|:---:|:-----------:|:---------------:|
| HTML       | ✓                     | ✓   | ✓           | ✓               |
| Markdown   | ×                     | ✓   | ✓           | ×               |
| Plain text | ×                     | ×   | ✓           | ×               |

I really preferred the HTML version, and went out of my way to find a [HTML reader plugin for Obsidian](https://github.com/nuthrash/obsidian-html-plugin).

### Skim

Website: [Skim download | SourceForge.net](https://sourceforge.net/projects/skim-app/)

**Step 0**: Make a backup copy of the PDF file in question

**Step 1**: Convert PDF annotations to Skim Notes: {{< menu `File` `Convert Notes…` `OK` >}}

At this point, all of the annotations are converted to Skim Notes, and will no longer appear in other PDF readers.

To export back, use {{< menu `File` `Export…` >}} and choose {{< menu `PDF` `With embedded notes` >}}. However, all the highlights and underlines now contain comments, just like Adobe Acrobat's {{< menu `Copy selected text into Highlight, Strike-Out, and Underline comment pop-ups` >}} option \([screenshots of Acrobat](https://softwarerecs.stackexchange.com/questions/9841/)\).

**Step 2**:  Export Notes: {{< menu `File` `Export…` >}}

In the {{< menu `File Format` >}} menu, selecting one of {{< menu `Notes as Text` >}}, {{< menu `Notes as RTF` >}}, {{< menu `Notes as RTFD` >}}, or {{< menu `Notes as FDF` >}} will export only the Notes.

Both plain text and RTF file only have the highlighted words and their page number, nothing else. I am not familiar with the other two formats.

> Since Skim provides [CLI tools](https://sourceforge.net/p/skim-app/wiki/Interaction_with_Skim/), I wonder whether there is a way to do everything in a programmatically. This repo [alexandergogl/SkimPDF](https://github.com/alexandergogl/SkimPDF) seems to do Step 1 but not Step 2.
{.book-hint .info}

### Partial exports: Obsidian/Zotero/Highlights

Main entries:

- [Obsidian](/computer/software-usage/obsidian/)
- [Zotero](/computer/software-usage/zotero/)

I have tried every existing plugin and/or built-in function that I could find with Obsidian and Zotero, but none of them exports annotations, only highlights and underlines. Same for [Highlights](https://highlightsapp.net/features/) \(I only tried the free {{< menu `Export Notes as PDF` >}} option which did not work. Hard to imagine that it would work for other formats\).

- [akaalias/obsidian-extract-pdf-highlights](https://github.com/akaalias/obsidian-extract-pdf-highlights/tree/master): Very buggy on Obsidian 1.4
- [jlegewie/zotfile](https://github.com/jlegewie/zotfile): Removed its {{< menu `Extract Annotations` >}} function after Zotero 6. Zotero 6's {{< menu `Add Note from Annotations` >}} function does not extract annotations.
- [stefanopagliari/bibnotes](https://github.com/stefanopagliari/bibnotes): Its {{< menu `Export Notes` >}} option uses notes from Zotero, yada yada yada.
- [windingwind/zotero-better-notes](https://github.com/windingwind/zotero-better-notes): Have to manually select and export every single note within Zotero's PDF viewer \(which I really don't like\), so I just lost interest and did not test if it handles annotations.


## Word count

[ezgranet/pdfwordcounter: PDF Word Counter](https://github.com/ezgranet/pdfwordcounter)

Very minimal GUI app, straight to the point.
