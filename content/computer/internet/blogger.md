---
weight: 400
title: "Blogger"
---
# Blogger

{{< hint danger >}}
I have stopped using Blogger. Proceed at your own risk.
{{< /hint >}}

Before switching to static site generator, I was a Blogger power user (if that is a thing). I basically learnt CSS because of wanting to make my Blogger prettier.

My old Blogger site is still online but no longer updated: [此生未命名 - Untitled Life](https://loikein.blogspot.com/)

## CSS

Everything:

```css
html {
  --theme: #CB455B;
  --theme-sub: #037BBA;
  --white: #FCFCFC;
  --black: #222;
  --dark-grey: #777;
  --grey: #E5E5E5;
  --code: #017B76;
}

/* link */

a, a:visited, .comment-link,
.widget.Profile .profile-link,
.widget.Profile .profile-link.visit-profile {
  color: var(--theme);
}

a:hover,
a:focus {
  color: var(--theme-sub);
}

.extendable .show-more,
.extendable .show-less {
  color: var(--theme);
  border-color: var(--theme);
}

/* sidebar & post body */

.pill-button {
  border-radius: 20px !important;
}

.blog-post,
.sidebar-container {
  background: var(--white);
}

.svg-icon-24 {
  display: none;
}

.post-body,
.widget.Profile .profile-link,
.widget.Profile dd,
.sidebar-container .widget .title {
  color: var(--black);
}

.profile-link.visit-profile.pill-button:hover,
.profile-link.visit-profile.pill-button:focus {
  color: var(--theme-sub);
}

/* tags */
.Label .label-count {
  float: none;
}

.byline.post-labels a, .Label a {
  color: var(--black);
  font-size: 0.7rem;
}

.byline.post-labels a, .Label li, .Label span.label-size {
  background: var(--grey);
  border: 1px solid var(--grey);
}

/* section title counter */
.post-body h2{
  counter-increment: counter_h2;
  counter-reset: counter_h3;
}

.post-body h2::before {
  content: counter(counter_h2)". ";
}

.post-body h3 {
  color: var(--black);
  counter-increment: counter_h3;
}

.post-body h3::before {
  content: counter(counter_h2)"."counter(counter_h3)". ";
}

/* humble hr line */
.post-body hr {
  border: 0;
  height: 1px;
  background: var(--black);
  background-image: linear-gradient(to right, var(--white),var(--black), var(--white));
}

/* link icon */
.post-body a::after {
  padding-left:2px;
  content: "\01F517";
}

/* block quote */
.post-body blockquote {
  padding: 1em 1em 1em 1em;
  background: var(--grey);
  line-height: 1.6em;
  color: var(--black);
}

/* inline-code beautifier */
.post-body code {
  color: var(--code);
  background: var(--grey);
  padding: 0.2em;
}

/* responsive iframe */

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

/* table */
.post-body table {
  margin: auto;
}

.post-body table,
.post-body table tr th,
.post-body table tr td {
  border: 1px solid var(--grey);
  border-collapse: collapse;
  padding: 0.4em;
  text-align: center
}

/* image */
/* reference: https://bradfrost.com/web/ */
.post-body img {
  border: 1px solid var(--dark-grey);
  box-shadow: 0 10px 0 -5px #e99095, 0 20px 0 -10px #f4b3b5, 0 30px 0 -16px #fbd7d7;
  margin-bottom: 1rem;
  margin-top: 0.5rem;
}

/* embedded gist normalization */
.gist table,
.gist table tr th,
.gist table tr td{
  border: 0px;
}

/* columns */
@media (min-width: 600px) {
  .col-wrap{
    display: grid;
    grid: auto-flow / 1fr 1fr;
    grid-column-gap: 1em;
}
```

### Accordion menu (pure CSS)

This was what became [accessible pure CSS accordion menu](https://github.com/loikein/literate-html/blob/master/CSS-form-input.md).

Blog (old): [工具箱](https://loikein.blogspot.com/p/useful-links.html)

Ref: [Pure CSS Accordion](https://codepen.io/raubaca/pen/PZzpVe)

```html
<style>
.accordion-box {
  overflow: hidden;
  padding-left:0;
}
.accordion {
  width: 100%;
  overflow: hidden;
  user-select: none;
}
.accordion-label {
  display: flex;
  justify-content: space-between;
  padding-right: 1em;
  cursor: pointer;
}
.accordion-label:hover {
  background-color: #dddddd;
}
.accordion-label::after {
  content: "\276F";
  text-align: center;
}
.accordion-content {
  max-height: 0;
  padding-right: 1em;
}
input {
  display: none;
}
input:checked + .accordion-label::after {
  -webkit-transform: rotate(90deg);
          transform: rotate(90deg);
}
input:checked ~ .accordion-content {
  max-height: 100vh;
}
</style>

<ul class="accordion-box">
<li class="accordion">
<input id="chck-1" type="checkbox" /><label class="accordion-label" for="chck-1">To-do list</label>
<ul class="accordion-content">
<li>Hello</li>
<li><strike>internet</strike></li>
<li>World!</li>
</ul>
</li>
</ul>
```

### Columns with CSS Grid

This was what became my first [column shortcode](https://github.com/loikein/hugo-theme-diary/blob/main/layouts/shortcodes/col.html).

```html
<style>
@media (min-width: 600px) {
  .col-wrap{
    display: grid;
    grid: auto-flow / 1fr 1fr;
    grid-column-gap: 1em;
}}
</style>

<div class="col-wrap"><div>
  你好，世界
</div><div>
  Hello, world
</div></div>
```

### Line number for tables

```css
table {
  counter-reset: tr-number;
}

tr>td:nth-child(1)::before{
  counter-increment: tr-number;
  content: counter(tr-number);
}
```

### Link box

Blog post:  
(old site) [把链接做成卡片形式：一个纯 html 的尝试（2019.7.10 更新截图网站）](https://loikein.blogspot.com/2018/11/html.html)  
(new site) [把链接做成卡片形式：一个纯 HTML 的尝试 - 此生未命名／Untitled Life](https://blog.loikein.one/posts/2018-11-28-card-links/)

Snippet for Create Link \(Chrome extension\):

```html
<style>%newline%
    .link-box { box-shadow:2px 2px 5px #DDD; }%newline%
    .link-box table{ border-collapse: collapse; margin: auto; }%newline%
    .link-box tr { border: 1px solid #DDD; text-align: left; }%newline%
    .link-box td { padding: 1em; border: 0px; text-align: left;}%newline%
</style>%newline%
<a href="%url%" target="_blank">%newline%
<table align=center class="link-box"><tr>%newline%
    <td width=160px>%newline%
        <img style="float:left;" src="https://thumbnail.ws/get/thumbnail/?apikey=ab45a17344aa033247137cf2d457fc39ee4e7e16a464&url=%url%" alt="" width="160" height="90" />%newline%
    </td>%newline%
    <td width=320px>%newline%
        %title%%newline%
    </td>%newline%
</tr></table></a><br />
```

Snippet for Link Text and Location Copier \(Firefox extension\):

```html
<style>%N
  .link-box { box-shadow:2px 2px 5px #DDD; }%N
  .link-box table{ border-collapse: collapse; margin: auto; }%N
  .link-box tr { border: 1px solid #DDD; text-align: left; }%N
  .link-box td { padding: 1em; border: 0px; text-align: left;}%N
</style>%N
<a href="%U" target="_blank">%N
  <table align=center class="link-box"><tr>%N
  <td width=160px>%N
    <img style="float:left;" src="https://thumbnail.ws/get/thumbnail/?apikey=ab45a17344aa033247137cf2d457fc39ee4e7e16a464&url=%linkurl%" alt="" width="160" height="90" />%N
  </td>%N
  <td width=320px>%N
  %T%N
  </td>%N
 </tr></table></a><br />
```

## Instagram widget page

New:

```html
<!-- SnapWidget -->
<script src="https://snapwidget.com/js/snapwidget.js"></script>
<iframe 
    src="https://snapwidget.com/embed/<your_id>" 
    class="snapwidget-widget" 
    allowtransparency="true" 
    frameborder="0" 
    scrolling="no" 
    style="border:none; 
           overflow:hidden; 
           width:100%; ">
</iframe>
```

Old:

```html
<div style="height: 16px;
           overflow: hidden; 
           padding-top: 100%; 
           position: relative; 
           width: 100%;">
<iframe 
    allowtransparency="true" 
    class="websta-widgets" 
    frameborder="0" 
    scrolling="no" 
    src="//widgets-code.websta.me/w/<your_id>"
    style="height: 100%; 
           left: 0; 
           position: absolute; 
           top: 0; 
           width: 100%;">
</iframe> 
<!-- WEBSTA WIDGETS - widgets.websta.me -->
</div>
```

## Syntax highlighting

I used to use [alexkay/hilite.me](https://github.com/alexkay/hilite.me).
