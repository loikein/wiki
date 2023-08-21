---
bookCollapseSection: true
title: CSS
---

My notes on CSS & HTML from ages ago \(in Japanese\): [notes: html 5 & css 3](https://gist.github.com/loikein/8af785feed5a265ca0cd936299178902)

## Responsive iframe

### New version (`aspect-ratio`)

```css
.video-container {
  width: 100%; /* this is not the actual width */
}

.video {
  width: 95%; /* this is the actual width */
}

.video--16x9{ aspect-ratio: 16/9; }
.video--4x3{ aspect-ratio: 4/3; }
```

Usage:

```html
<div class="video-container">
  <iframe
  class="video video--4x3"
  src="https://www.youtube-nocookie.com/embed/<video_id>?cc_load_policy=1&cc=1" allowfullscreen title="YouTube video" frameborder="0" sandbox="allow-same-origin allow-scripts" loading="lazy"></iframe>
</div>
```

### Old version (`padding-bottom`)

Ref: [Responsive iframes — The Right Way (CSS Only)! | Ben Marshall](https://www.benmarshall.me/responsive-iframes/)

```css
.video-container{
  position: relative;
  height: 0;
}
    
.video-container--4x3{ padding-bottom: 75%; }
.video-container--16x9{ padding-bottom: 56.25%; }

.video-container iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
```

Usage:

```html
<div class="video-container video-container--4x3">
  <iframe src="https://www.youtube-nocookie.com/embed/<video_id>?cc_load_policy=1&cc=1" allowfullscreen title="YouTube video" frameborder="0" sandbox="allow-same-origin allow-scripts" loading="lazy"></iframe>
</div>
```

## Random shadow animation

…that I somehow made for something.

```css
.shadow {
  box-shadow: 0 .5rem 0 rgba(0,0,0,.15);
  transition: transform 0.2s, box-shadow 0.2s;
}

.shadow:hover {
  box-shadow: 0 0.7rem 0 rgba(0,0,0,.2);
  transform: translateY(-0.2rem);
  transition: transform 0.2s, box-shadow 0.2s;
}
```

## Skip-to-main button

Credit: [Hidden content for better a11y | Go Make Things](https://gomakethings.com/hidden-content-for-better-a11y/#hiding-the-link)

CSS:

```css
.screen-reader {
  border: 0;
  clip: rect(0 0 0 0);
  height: 1px;
  margin: -1px;
  overflow: hidden;
  padding: 0;
  position: absolute;
  white-space: nowrap;
  width: 1px;
}

.screen-reader-focusable:active,
.screen-reader-focusable:focus {
  display: block;       /* added */
  text-align: center;   /* added */
  clip: auto;
  height: auto;
  margin: 0;
  overflow: visible;
  position: static;
  white-space: normal;
  width: auto;
}
```

Usage:

```html
<body>
  <a class="screen-reader screen-reader-focusable" href="#main">Skip to the main content</a>
  <nav>Navigation elements...</nav>
  <main id="main">The main content</main>
  ...
</body>
```

## Queries

Refs:

- [CSS Style Queries - Ahmad Shadeed](https://ishadeed.com/article/css-container-style-queries/)
