---
weight: 200
title: "Custom CSS"
---
# Custom CSS

For usage see: [Browser extension #Customise the web](/computer/internet/browser-extension/#customise-the-web)

Some of the bugs may have been caused by my browser settings. Adopt after careful inspection.

## Universal

Range: Everything

```css
s, strike, del {
    opacity: 60%;
}
```

## AO3

Range: URLs on the domain: `archiveofourown.org`

```css
/* limit line length */
#main {
    max-width: 700px;
}
```

{{< details "Dark theme" >}}
{{< hint info >}}
This is AO3's [official dark theme](https://archiveofourown.org/skins/929), but applying it automatically (also works on mobile devices) requires logging-in and some setups, which I recommend doing. If you were able to use it, you can safely ignore the following section.
{{< /hint >}}

```css
/* dark theme */
@media (prefers-color-scheme: dark) {
#outer .region,
#footer .group,
.post fieldset fieldset,
fieldset fieldset {
  background: none;
}

body,
.group,
.group .group,
.region,
.flash,
fieldset,
fieldset fieldset ul,
form dl,
textarea,
#main .verbose legend,
.verbose fieldset,
.notice,
ul.notes,
input,
textarea,
table,
th,
td:hover,
tr:hover,
.symbol .question:hover,
#modal,
.ui-sortable li,
.required .autocomplete,
.autocomplete .notice,
.system .intro,
.comment_error,
.kudos_error,
div.dynamic,
.dynamic form,
#ui-datepicker-div,
.ui-datepicker table {
  background: #333;
  color: #eee;
  border-color: #222;
  outline: #111;
  box-shadow: none;
}

#header .actions a:hover,
#header .actions a:focus,
#header .dropdown:hover a,
#header .open a,
#header .menu,
#small_login,
.group.listbox,
fieldset fieldset.listbox,
form blockquote.userstuff,
input:focus,
textarea:focus,
li.relationships a,
.group.listbox .index,
.dashboard fieldset fieldset.listbox .index,
#dashboard a:hover,
th,
#dashboard .secondary,
.secondary,
.thread .even,
.system .tweet_list li,
.ui-datepicker tr:hover {
  background: #2a2a2a;
}

#header .dropdown .menu a:hover,
#header .dropdown .menu a:focus,
.splash .favorite li:nth-of-type(odd) a,
.ui-datepicker td:hover,
#tos_prompt .heading,
#tos_prompt [disabled] {
  background: #111;
}

#outer,
.javascript,
.statistics .index li:nth-of-type(even),
#tos_prompt,
.announcement input[type="submit"] {
  background: #333;
}

#header ul.primary,
#outer #footer,
.toggled form {
  background: url("/images/skins/textures/tiles/black-noise.jpg");
}

#header ul.primary,
#footer,
#dashboard ul,
dl.meta,
.group.listbox,
fieldset fieldset.listbox,
#main li.blurb,
form blockquote.userstuff,
div.comment,
li.comment,
.toggled form,
form dl dt,
form.single fieldset,
#inner .module .heading,
.bookmark .status span,
.splash .news li,
.filters .group dt.bookmarker {
  border-color: #555;
}

.group.listbox,
fieldset fieldset.listbox,
#main li.blurb,
.wrapper,
#dashboard .secondary,
.secondary,
form blockquote.userstuff,
.thread .comment,
.toggled form {
  box-shadow: 1px 1px 3px #000;
}

#dashboard .current,
.actions a:active,
#outer .current,
a.current,
.current a:visited,
span.unread,
.replied,
span.claimed,
dl.index dd,
.own,
.draft,
.draft .unread,
.child,
.unwrangled,
.unreviewed,
.ui-sortable li:hover {
  background: #000;
  border-color: #555;
  box-shadow: -1px -1px 3px #000;
}

input,
textarea {
  box-shadow: inset 0 1px 2px #000;
}

li.blurb,
.blurb .blurb,
.listbox .index,
fieldset fieldset.listbox,
.dashboard .listbox .index {
  box-shadow: inset 1px 1px 3px #000;
}

#footer a:hover,
#footer a:focus,
.autocomplete .dropdown ul li:hover,
.autocomplete .dropdown li.selected,
a.tag:hover,
.listbox .heading a.tag:visited:hover,
.symbol .question,
.qtip-content {
  background: #5998D6;
  color: #111;
}

.splash .favorite li:nth-of-type(odd) a:hover,
.splash .favorite li:nth-of-type(odd) a:focus {
  background: #5998D6;
  color: #111;
}

#header #greeting img,
#header .heading a,
#header .heading a:visited,
#header .user a:hover,
#header .user a:focus,
#header fieldset,
#header form,
#header p,
#dashboard a:hover,
.actions a:hover,
.actions input:hover,
.delete a,
span.delete,
span.unread,
.replied,
span.claimed,
.draggable,
.droppable,
span.requested,
a.work,
.blurb h4 a:link,
.blurb h4 img,
.splash .module h3,
.splash .browse li a:before,
.required,
.error,
.comment_error,
.kudos_error,
a.cloud7,
a.cloud8,
#tos_prompt .heading {
  color: #5998D6;
}

#greeting .icon,
#dashboard,
#dashboard.own,
.error,
.comment_error,
.kudos_error,
.LV_invalid,
.LV_invalid_field,
input.LV_invalid_field:hover,
input.LV_invalid_field:active,
textarea.LV_invalid_field:hover,
textarea.LV_invalid_field:active,
.qtip-content {
  border-color: #5998D6;
}

a,
a:link,
a.tag,
#header a,
#header a:visited,
#header .primary .open a,
#header .primary .dropdown:hover a,
#header .primary .dropdown a:focus,
#header #search input:focus,
#header #search input:hover,
#dashboard a,
#dashboard span,
#dashboard .current,
.heading,
.group .heading,
.filters dt a:hover {
  color: #fff;
}

a:visited,
.actions a:visited,
.action a:link,
.action a:visited,
.listbox .heading a:visited,
span.series .divider {
  color: #999;
}

.actions a,
.actions a:link,
.action,
.action:link,
.actions input,
input[type="submit"],
button,
.current,
.actions label,
#header .actions a {
  background: #555;
  border-color: #222;
  color: #eee;
  box-shadow: inset 0 -8px 4px #232323, inset 0 8px 7px #555;
  text-shadow: none;
}

.actions a:hover,
.actions input:hover,
#dashboard a:hover,
.actions a:focus,
.actions input:focus,
#dashboard a:focus,
.actions .disabled select {
  color: #999;
  border-color: #000;
  box-shadow: inset 2px 2px 2px #000;
}

.actions a:active,
.current,
a.current,
.current a:visited {
  color: #fff;
  background: #555;
  border-color: #fff;
  box-shadow: inset 1px 1px 3px #333;
}

.delete a,
span.delete {
  box-shadow: -1px -1px 2px rgba(255,255,255.25);
}

.actions label.disabled {
  background: #222;
  box-shadow: none;
}

ul.required-tags,
.bookmark .status span,
.blurb .icon {
  opacity: 0.9;
  border: 0;
}

#outer .group .heading,
#header .actions a,
fieldset.listbox .heading,
.userstuff .heading,
.heading,
.userstuff h2 {
  text-shadow: none;
  color: #fff;
  background: none;
}

#header .actions a,
fieldset fieldset,
.mce-container button,
.filters .expander,
.actions .disabled select {
  box-shadow: none;
}

fieldset fieldset.listbox {
  outline: none;
}

form dd.required {
  color: #eee;
}

.mce-container input:focus {
  background: #F3EFEC;
}

.announcement .userstuff a,
.announcement .userstuff a:link,
.announcement .userstuff a:visited:hover {
  color: #111;
}

.announcement .userstuff a:visited {
  color: #666;
}

.announcement .userstuff a:hover,
.announcement .userstuff a:focus {
  color: #999;
}

.event.announcement .userstuff a,
.filters .expander {
  color: #eee;
}
}
```

{{< /details >}}

## GitHub

Range: URLs on the domain: `github.com`

```css
body {
    padding-right: 0 !important; /* Firefox search field bug */
}

del {
    color: grey;
}

.markdown-body img {
    border: 1px var(--color-border-default) solid;
}

#symbols-button,
.convert-to-issue-button,
.drag-handle {
    display: none !important;
    visibility: collapse;
}

.js-blob-wrapper {
    overflow-x: unset !important;
}

.merge-status-list {
    max-height: unset !important;
    overflow: auto;
}

.comment-body {
    font-size: 16px;
}

/* sticky side bars */

#partial-discussion-sidebar,
.h-card {
    position: sticky !important;
    top: 54.5px;
}

.BorderGrid,
.js-repo-nav {
    position: sticky !important;
    top: 0;
}
```

Range: URLs matching the regexp: `.*github\.com/.*/.*/pull/.*`

```css
/* hide inline annotation option when looking at PR */
.js-inline-annotations {
    display: none;
    visibility: collapse;
}
```

## Office Online

Range: URLs on the domain: `officeapps.live.com` (particularly within iframes)

```css
/* color tweaks for cell in focus */

:root {
  --highlight-color: purple; /* original: #217346 */
  --cell-border: 4px;
  --row-col-border: 2px;
}

.ewrch-row-cellsel, .ewrch-col-cellsel, .ewrch-row-sel, .ewrch-col-sel {
  color: var(--highlight-color);
}

.ewr-selection-fillhandle {
  width: calc(2 * var(--cell-border));
  height: calc(2 * var(--cell-border));
  bottom: calc(-2 * var(--cell-border) + 2px);
  background-color: var(--highlight-color);
}

.ewr-grdcontarea-ltr .ewr-selection-fillhandle {
  right: -8px;
}

.ewr-cell-selection-highlight-all,
.ewr-discontinuous-selection-active-cell,
.ewr-cell-presence-highlight-all,
.ewr-cell-presence-highlight-edit,
.ewr-cell-sharing-highlight {
  border: var(--cell-border) solid var(--highlight-color);
}

.ewr-cell-selection-highlight-rows,
.ewr-grdcontarea-ltr .ewr-cell-selection-highlight-cols,
.ewr-grdcontarea-rtl .ewr-cell-selection-highlight-rows {
  border: var(--row-col-border) solid var(--highlight-color) !important;
}

.ewr-grdcontarea-ltr .ewr-marquee-selection-highlight,
.ewr-grdcontarea-ltr .ewr-rangepicker-selection-highlight-dashed,
.ewr-grdcontarea-ltr .ewr-cell-selection-highlight-all,
.ewr-grdcontarea-ltr .ewr-selection-filldragborder,
.ewr-grdcontarea-ltr .ewr-cell-presence-highlight-all,
.ewr-grdcontarea-ltr .ewr-cell-presence-highlight-edit {
  margin: calc(-1 * var(--cell-border)) 0 0 calc(-1 * var(--cell-border));
}
```

```css
/* add extra border for row & col in focus */

.ewrch-row-cellsel::before,
.ewrch-row-cellsel::after,
.ewr-cell-selection-highlight-cols::before,
.ewr-cell-selection-highlight-cols::after {
  content: '';
  clear: both;
  background: var(--highlight-color);
  display: block;
  position: absolute;

}

.ewrch-row-cellsel::before,
.ewrch-row-cellsel::after {
  left: 0;
  width: 100px;
  height: var(--cell-border);
}

.ewr-cell-selection-highlight-cols::before,
.ewr-cell-selection-highlight-cols::after {
  top: -19px;
  width: var(--cell-border);
  height: 100px;
}

.ewrch-row-cellsel::before{ top: calc(-1 * var(--cell-border)); }
.ewrch-row-cellsel::after{ top: 19px; }
.ewr-cell-selection-highlight-cols::before { left: calc(-1 * var(--cell-border)); }
.ewr-cell-selection-highlight-cols::after { left: 49px; }
```

## Python documentations

Range: URLs on the domain: `pandas.pydata.org`, `numpy.org`

```css
/* highlight param names */
dt strong {
  color: var(--pst-color-primary);
}
```

Range: URLs on the domain: `pythonhosted.org`

```css
/* highlight param names */
ul li strong {
    color: #3fb79c;
}
```

Range: URLs on the domain: `statsmodels.org`

```css
/* highlight param names */
dt strong {
  color: var(--md-primary-fg-color);
}
dt .classifier a {
  color: unset;
}

/* unset scroll bar highlight */
.md-typeset pre > code,
.md-typeset pre > code:hover {
  scrollbar-color: unset;
}
```

## Wayback Machine

Range: URLs on the domain: `web.archive.org`

```css
/* improve a11y on older sites */
:focus:not([tabindex="-1"]) {
  outline: 5px solid #CF3643;
  outline-offset: 1px;
  border: 0;
}
```
