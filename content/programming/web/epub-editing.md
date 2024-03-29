---
title: "EPUB editing"
---

## Alignment

### Vertical align

[html - How do I vertically center text with CSS? - Stack Overflow](https://stackoverflow.com/questions/8865458/how-do-i-vertically-center-text-with-css)


{{< details "Method: `padding-top: 25vh`" >}}
TBE

{{< /details >}}

{{< details "Method: table" >}}
Ref: [MobileRead Forums - View Single Post - How do you vertically center a text?](https://www.mobileread.com/forums/showpost.php?p=2616843&postcount=4)

Page code:

```html
<body>
<div class="part-page">
  <div class="top_row"></div>

  <div class="middle_row">
  <h1>...</h1>
  </div>

  <div class="bottom_row">
  <h2>...</h2>
  </div>
</div>
</body>
```

CSS:

```css
.part-page {
  display: table;
  height: 100%;
  width: 100%;
  text-indent: 0;
  text-align: center;
}

.top_row {
  display: table-row;
  height: 15%;
}

.middle_row {
  display: table-row;
  height: 70%;
}

.bottom_row {
  display: table-row;
  height: 15%;
}

.middle_row h1 {
  display: table-cell;
  vertical-align: middle;
  text-align: center;
  text-indent: 0;
  font-size: 1.4em;
}

.bottom_row h2 {
  display: table-cell;
  vertical-align: middle;
  text-align: center;
  text-indent: 0;
}
```
{{< /details >}}



{{< details "Method: margin \& transform" >}}
Ref: [Vertically Centered Text in iBooks – EPUBSecrets](https://epubsecrets.com/vertically-centered-text-in-ibooks.php)

> This method looks good when it works, but horrible when it doesn't work. Be aware.
{.book-hint .warning}

Page code:

```html
<body>
  <div class="vertical-center">
    <h1>...</h1>
  </div>
</body>
```

CSS:

```css
.vertical-center {
  margin: 50vh 0 0 0;
  text-align: center;
  -webkit-transform: translateY(-50%);
  transform: translateY(-50%);
}
```
{{< /details >}}


## Image sizing

### Full-page images


### Small block images

Refs:

- [keeping small images small in an epub - MobileRead Forums](https://www.mobileread.com/forums/showthread.php?t=336576#postcount4082496)
- [epub - CSS image sizing - Stack Overflow](https://stackoverflow.com/a/19759941/10668706)

**Problem: allowing images to scale down, while limiting the maximum size, and horizontally centred in page.**

Page code:

```html {hl_lines="3-5 7"}
<div class="chapter-image-wrapper">
  <svg
    style="max-width:[desired-width]px; max-height:[desired-height]px"
    viewBox="0 0 [actual-width] [actual-height]"
    preserveAspectRatio="xMidYMid meet"
    xmlns="http://www.w3.org/2000/svg" version="1.1" xmlns:xlink="http://www.w3.org/1999/xlink" >
    <image width=[actual-width] height=[actual-height] xlink:href="../Images/pic.png"/>
    <!-- Warning: Kobo will not display the image without the width & height in the image tag -->
  </svg>
</div>
```

CSS:

```css
div.chapter-image-wrapper {
  margin: 0;
  page-break-inside:avoid;
  padding: 0;
  text-align: center;
  text-indent: 0;
}
```


### Small inline images

Page code: \(all in one line, inside the line\)

```html
<span class="chapter-emoji-wrapper">
  <svg viewBox="0 0 54 51" preserveAspectRatio="xMidYMid meet" xmlns="http://www.w3.org/2000/svg"  version="1.1" xmlns:xlink="http://www.w3.org/1999/xlink" >
    <image width=[actual-width] height=[actual-height] xlink:href="../Images/emoji.png"/>
  </svg>
</span>
```

CSS:

```css
span.chapter-emoji-wrapper {
  margin: 0;
  padding: 0;
}

span.chapter-emoji-wrapper svg {
  max-width: 1em;
  max-height: 1em;
  margin: 0;
  padding: 0;
}
```

## Footnotes

Refs:

- [Apple Books Pop-up Footnotes](https://help.apple.com/itc/booksassetguide/en.lproj/itccf8ecf5c8.html)
- [FR: "Show endnotes as footnotes." · Issue #9780 · koreader/koreader](https://github.com/koreader/koreader/issues/9780)
