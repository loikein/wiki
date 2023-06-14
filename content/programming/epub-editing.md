---
title: "EPUB editing"
---
# EPUB editing

## Image sizing

### Small inline images

Refs:

- [keeping small images small in an epub - MobileRead Forums](https://www.mobileread.com/forums/showthread.php?t=336576#postcount4082496)
- [epub - CSS image sizing - Stack Overflow](https://stackoverflow.com/a/19759941/10668706)

**Problem: allowing images to scale down, while limiting the maximum size, and keep centred in page.**

Page code:

```html
<div class="chapter-image-wrapper">
  <svg style="max-width:<width-of-pic>px; max-height:<height-of-pic>px" xmlns="http://www.w3.org/2000/svg" height="100%" width="100%" preserveAspectRatio="xMidYMid meet" version="1.1" viewBox="0 0 <width-of-pic> <height-of-pic>" xmlns:xlink="http://www.w3.org/1999/xlink" >
    <image xlink:href="../Images/pic.png"/>
  </svg>
</div>
```

CSS code:

```css
div.chapter-image-wrapper {
  margin: 0;
  page-break-inside:avoid;
  padding: 0;
  text-align: center;
  text-indent: 0;
}
```
