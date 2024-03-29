---
weight: 400
title: "Obsidian"
---

> I use Obsidian with macOS 10.15 Catalina, iOS 17, and iPadOS 15. Unless stated otherwise, everything mentioned here should work everywhere.
> 
> If some plugin does not actually work on mobile, but it tries to load every time nonetheless, putting `"isDesktopOnly": true` in `vault/.obsidian/plugins/plugin-name/manifest.json` will turn it off on mobile.
{.book-hint .info}

## Admin

### Sync between devices

Do not use iCloud WITH git. Pick one.


### Working with multiple vaults

Set a different accent colour for each vault for a more obvious visual reminder.


## Settings

### Hotkeys to add

Toggle blockquote: {{< kbd `command` `shift` `.` >}} \([Ref](https://old.reddit.com/r/ObsidianMD/comments/nkz24v/is_there_a_hotkey_to_toggle_a_block_quote/)\)


## Cursor

### Snippet to partially increase cursor thickness

The characters are not typos!

{{< details "Reference: Core styles of the default cursors, obtained from inspection" >}}
{{< highlight-file file="default-cursor.css" lang="css" >}}
{{< /details >}}

There are two types of cursors, `.cm-cursor` \(end-border of selection\) and `.cm-dropCursor` \(caret when user is typing\). The following style only works on the former, using accent colour from iB theme, with default accent as fallback.

{{< highlight-file file="-cursor.css" lang="css" >}}

### Ninja cursor

Repo: [vrtmrz/ninja-cursor](https://github.com/vrtmrz/ninja-cursor)

After making little changes to [this comment](https://github.com/vrtmrz/ninja-cursor/issues/3#issuecomment-1806902738) in the Ninja cursor repository, I finally feel like this plugin could be a serious default cursor alternative \(**on desktop**\). Still not perfect, because the huge cursor bar on left when you select multiple lines still exists, but during typing it is a much more pleasant experience than the default cursor.

> Notes for Obsidian iOS:
> 
> 1. When made thick and tall enough, the x-cursor will cover \(not replace\) the blinking cursor on iOS as well. The numbers below are tested minimals for this purpose.
> 2. After launching Obsidian, the plugin takes a few seconds \(I guess maybe even on some less powerful desktop devices\) to start-up, before which you will see the default cursor;
> 3. During scrolling, the x-cursor will stay at its on-screen position \(as opposed to: in-text position\) for a split second, and may stay there until tapping at a new position. If your main writing device is iOS, this is experience-breaking.
{.book-hint .danger}

If you want to use this solution, disable the previous cursor snippet, and add the following instead. I changed the width and height, and the blinking animation. You cannot write `animation: none` to stop it, because that will leave you with no cursor. Unfortunately I think it is just how this plugin works.

{{< highlight-file file="plugin-ninja-cursor.css" lang="css" >}}


## Focus \(zen\) mode / typewriter scroll

### Focus Active Sentence

Repo: [artisticat1/focus-active-sentence: Highlight the active sentence in Obsidian.md](https://github.com/artisticat1/focus-active-sentence)

Focus on the current sentence. The focus disappears when scrolling or changing lines.

To accommodate writing in Chinese, preferences:

- Sentence delimiters: `。？！` 
- Extra characters: `%~*”」`

### Ghost Fade Focus

Repo: [skipadu/obsidian-ghost-fade-focus: Ghost Fade Focus plugin for Obsidian](https://github.com/skipadu/obsidian-ghost-fade-focus)

> This plugin **will** work on Obsidian for iOS \(v1.4.16\) on iPadOS 15, after setting `isDesktopOnly: false` in `vault/.obsidian/plugins/ghost-fade-focus/manifest.json`.
{.book-hint .info}

Gradient focus mode on every 5 lines \(or every paragraph\) above and below the cursor.

### Scroll Offset

Repo: [lijyze/scroll-offset: Scroll Offset for Obsidian](https://github.com/lijyze/scroll-offset)

> This plugin does not work on iOS as of now.
{.book-hint .warning}

### Stille

Repo: [michaellee/stille](https://github.com/michaellee/stille)

Focus on the current paragraph.

Click the moon icon in the [Ribbon](https://help.obsidian.md/User+interface/Workspace/Ribbon), or use {{< menu `Command palette` `Stille: Toggle Stille` >}} to activate.

### Typewriter Mode

Repo: [davisriedel/obsidian-typewriter-mode](https://github.com/davisriedel/obsidian-typewriter-mode)

New, still testing out. Seems to consume a lot of memory…

### Typewriter Scroll

Repo: [deathau/cm-typewriter-scroll-obsidian: Typewriter Scroll Obsidian Plugin](https://github.com/deathau/cm-typewriter-scroll-obsidian)

> This plugin **does** work on Obsidian for iOS \(v1.4.16\) on iPadOS 15, but sometimes a little buggy when scrolling.
{.book-hint .info}

Has a built-in zen mode, which focuses on the current paragraph.

On desktop, the focus does not disappear unless switch to another software. On mobile, the focus only appears after tapping at a note and the keyboard's appearing.

Use {{< menu `Command palette` `Typewriter Scroll: Toggle On/Off` >}} to activate scrolling, and use {{< menu `Command palette` `Typewriter Scroll: Toggle Zen Mode On/Off` >}} to activate focus mode.


## Showing whitespace \(control characters)

### Show Whitespace

Repo: [deathau/cm-show-whitespace-obsidian](https://github.com/deathau/cm-show-whitespace-obsidian)

{{< details "Reference: Core styles of this plugin, obtained from inspection" >}}
Source: [deathau/cm-show-whitespace-obsidian/styles.scss](https://github.com/deathau/cm-show-whitespace-obsidian/blob/main/styles.scss)

{{< highlight-file file="cm-show-whitespace-core.css" lang="css" >}}
{{< /details >}}

Because this plugin has been unmaintained for a while, a patch is needed to make everything look consistent. Add a CSS file with the following contents: \(the `<br>` style came from [here](https://stackoverflow.com/a/64912130)\)

{{< highlight-file file="plugin-show-whitespace.css" lang="css" >}}

### Control Characters

Repo: [joethei/obsidian-control-characters](https://github.com/joethei/obsidian-control-characters)

When I was looking for an alternative of [cm-show-whitespace-obsidian](#cm-show-whitespace-obsidian), I found this plugin which also integrates with [mgmeyers/obsidian-style-settings](https://github.com/mgmeyers/obsidian-style-settings) to make customising possible without fiddling with CSS files. However, I did not like the default SVGs, and could not bother with finding new SVGs right now, so I am still using the old plugin.

### Show Whitespace \(CM6\)

Repo: [ebullient/obsidian-show-whitespace-cm6](https://github.com/ebullient/obsidian-show-whitespace-cm6)

This plugin is buggy with line breaks \([Issue #83](https://github.com/ebullient/obsidian-show-whitespace-cm6/issues/83)\), but it complements deathau/cm-show-whitespace-obsidian in the sense that it shows spaces (`␣`) very well. Following is setting and CSS styles for using them together.

- Show Whitespace
	- Toggle Show Whitespace: True
  - Show space characters: False
  - Show single space characters: False
  - Show trailing space characters: False
  - Show newline characters: True
  - Show strict line break characters: True
  - Show tab characters: False
- Show Whitespace \(CM6\)
	- Suppress plugin styles: True
	- Always show blockquote markers: \(any\)
	- Show all whitespace characters in code blocks: True
	- Show all whitespace characters: True
	- Outline list markers: \(any\)

{{< highlight-file file="plugin-show-whitespace-cm6.css" lang="css" >}}


## Plugins \(for peaceful writing\)

Most of my creative writings are in Chinese and published under my other online personae.

### Copy as HTML

Repo: [jenningsb2/copy-as-html: A simple plugin that copies the selected text to your clipboard as HTML](https://github.com/jenningsb2/copy-as-html)

> This plugin does not work on iOS as of now.
{.book-hint .warning}

After some initial testing, I found this plugin better than [Copy Document as HTML](https://github.com/mvdkwast/obsidian-copy-as-html), in the sense that it can be configured to remove comments at copy. However, neither adds right-click context menu.

### Hider

Repo: [kepano/obsidian-hider](https://github.com/kepano/obsidian-hider)

Hide ribbon, vault name, file explorer icons when in writing mode.

### Hover Editor

Repo: [nothingislost/obsidian-hover-editor](https://github.com/nothingislost/obsidian-hover-editor)

Need to turn on the core Page Preview plugin first, or force reload.

Together with `![[]]` embed, and setting hotkeys {{< kbd `option` `↑` >}} and {{< kbd `option` `↓` >}} for swap lines \(credit: [@seviche@kongwoo.icu](https://kongwoo.icu/users/seviche)\) makes an ok block-editing environment[^ulysses].

[^ulysses]: Yes, I am still missing the Ulysses block editing feature.

### Iconize

Repo: [FlorianWoelki/obsidian-iconize: Simply add icons to anything you want in Obsidian.](https://github.com/FlorianWoelki/obsidian-iconize)

To visually indicate the status of a piece of writing in the file tree. Set icon font size to be 1px smaller than the current font size.

I personally found the open source [Lucide Icons](https://lucide.dev/icons/) \(and [BoxIcons](https://boxicons.com/), but it has less options\) pack aesthetically pleasing and easy to see even on mobile. Also, Twemoji.

### Longform

Repo: [kevboh/longform: A plugin for Obsidian that helps you write and edit novels, screenplays, and other long projects.](https://github.com/kevboh/longform)

I just wanted to automatically create a multi-chapter project, not really needing any of the compilation functionalities. Turns out it can also create single-chapter project, but ignores the scene template when doing so.

Articles for reference:

- [Writing a novel in Markdown - pdworkman.com](https://pdworkman.com/writing-a-novel-in-markdown/) \(With file structure and plugin recommendations for complex commercial projects\)
- [Writing Long Form Content With Obsidian](https://www.eleanorkonik.com/writing-long-form-content/)


### Novel Word Count

Repo: [isaaclyman/novel-word-count-obsidian: Obsidian plugin. Displays a word count or other statistic for each file, folder and vault in the File Explorer pane.](https://github.com/isaaclyman/novel-word-count-obsidian)

Preferences:

- Notes
  + First type: Word count
  + Suffix: `字`
  + Alignment: Right-aligned
- Folders
  + First type: None
- Show advanced options: True
  - Exclude comments: True
  - Word count method: Han/Kana/Hangul (CJK) \(Note: Using this option will exclude any non-CJK words when counting\)

### Quiet Outline

Repo: [guopenghui/obsidian-quiet-outline](https://github.com/guopenghui/obsidian-quiet-outline)

> This plugin never loads successfully on my iOS devices.
{.book-hint .warning}

Use {{< menu `Command palette` `Quiet Outline: Quiet Outline` >}} to activate if did not auto-load.

Preferences:

- Search Support: False
- Level Switch: False
- Default Level: `H5`
- Auto Expand: False \(important for the Default Level to take effect\)
- Drag headings to modify note: True \(for a pseudo block editing experience\)

Some styles I wrote for more obvious current entry highlighting:

{{< highlight-file file="plugin-quiet-outline.css" lang="css" >}}


## Plugins \(for aggressive note-taking\)

Any combination of plugins in the previous sector, plus…

### EPUB readers that I am trying out

- [elias-sundqvist/obsidian-annotator: A plugin for reading and annotating PDFs and EPUBs in obsidian.](https://github.com/elias-sundqvist/obsidian-annotator) \(Very fragile; doesn't work on iOS 16.3 or higher.\)
- [AwesomeDog/obsidian-awesome-reader: Make Obsidian a proper Reader.](https://github.com/AwesomeDog/obsidian-awesome-reader/tree/master)
- [caronchen/obsidian-epub-plugin: An ePub reader plugin for Obsidian.](https://github.com/caronchen/obsidian-epub-plugin/tree/master)
- Using calibre Content server: [Workflow : Reading Ebook(epub, mobi, azw, etc ) in Obsidian - Share & showcase - Obsidian Forum](https://forum.obsidian.md/t/workflow-reading-ebook-epub-mobi-azw-etc-in-obsidian/17977/12)

### Full Calendar

Repo: [davish/obsidian-full-calendar: Keep events and manage your calendar alongside all your other notes in your Obsidian Vault.](https://github.com/davish/obsidian-full-calendar)

I only use it to display my [iCloud calendar](https://davish.github.io/obsidian-full-calendar/calendars/caldav/) \(read-only\), but obviously it is far more powerful than that.

### HTML Reader

Repo: [nuthrash/obsidian-html-plugin: This is a plugin for Obsidian (https://obsidian.md). Can open document with .html and .htm file extensions.](https://github.com/nuthrash/obsidian-html-plugin)

Add the ability to read \(no edit\) `.html` files in Obsidian.

### Link Favicons

Repo: [joethei/obsidian-link-favicon: See the favicon for a linked website.](https://github.com/joethei/obsidian-link-favicon?tab=readme-ov-file)

Add favicons before or after links for better scan-ability.

### Linter

Repo: [platers/obsidian-linter: An Obsidian plugin that formats and styles your notes with a focus on configurability and extensibility.](https://github.com/platers/obsidian-linter)

Cannot live without `line-break-at-document-end`.

### List Callouts

Repo: [mgmeyers/obsidian-list-callouts: Create callouts in lists in Obsidian.](https://github.com/mgmeyers/obsidian-list-callouts)

Very very useful, highly recommended.

Seems not compatible with checklists. My tweaks:

- !! red
- ! orange
- ? yellow
- y green
- n grey

### Number Headings

Repo: [onlyafly/number-headings-obsidian: Automatically number headings in a document in Obsidian](https://github.com/onlyafly/number-headings-obsidian)

> 1. It takes a long time for the Obsidian TOC to update after changing the numbers, if you have a relatively large file \(\~ 10KB\).
> 2. Adding new headings requires a manual off-on refresh, or a few seconds of waiting time in auto mode.
{.book-hint .warning}

Preferences:

- First heading level: `2`
- Separator style: `.`

### Prominent \(Starred\) Files

Repo: [javalent/prominent-files: Prominently display starred files in Obsidian.md](https://github.com/javalent/prominent-files/tree/main)

> Bug: On iOS, every time launch Obsidian, need turn the plugin off and on again to take effect.
{.book-hint .info}

Adds a bookmark symbol to the bookmarked notes in the file tree.

Companion snippet by me:

{{< highlight-file file="plugin-prominent-files.css" lang="css" >}}

### Unitade

Repo: [Falcion/UnitadeOBSIDIAN: A plugin for note-taking app Obsidian™ which allows you to treat any file extension as markdown note-file](https://github.com/Falcion/UnitadeOBSIDIAN)

Add the ability to read and edit `.txt` files in Obsidian.

### Zotero integration

Repo: [mgmeyers/obsidian-zotero-integration: Insert and import citations, bibliographies, notes, and PDF annotations from Zotero into Obsidian.](https://github.com/mgmeyers/obsidian-zotero-integration/tree/main)

Ref: [An Updated Academic Workflow: Zotero & Obsidian | by Alexandra Phelan | Medium](https://medium.com/@alexandraphelan/an-updated-academic-workflow-zotero-obsidian-cffef080addd) \(The Pandoc Reference List plugin had some weird bugs on my setup.\)

> With this plugin installed and enabled, launching Obsidian on an iPad without Zotero installed will disable it for both mobile and desktop. I have not tried with a device where Zotero is installed, but GitHub issues regarding mobile usage suggests it should work.
{.book-hint .warning}


## Other plugins that I have tried

### Better Word Count

Repo: [lukeleppan/better-word-count: Counts the words of selected text in the editor.](https://github.com/lukeleppan/better-word-count)

Replaces the core word count plugin in status bar. I did not actually need so many options. If you have the same need as me, just use the [#Hide word count](#hide-word-count-in-word-count-plugin) snippet. However, I think this plugin does have the extra option to exclude comments, which I don't write a lot of.

My only problem with the core word count is that it should exclude the front matter, [but that seems to be on the roadmap already](https://forum.obsidian.md/t/word-count-based-on-preview-rendered-text-not-editor-text/4758/18).

### Recent Files

Repo: [tgrosinger/recent-files-obsidian: Display a list of most recently opened files](https://github.com/tgrosinger/recent-files-obsidian)

As a second pane in the left split. [Cannot sync between devices](https://github.com/tgrosinger/recent-files-obsidian/issues/46) as of now, which is a little annoying.

### TagFolder

Repo: [vrtmrz/obsidian-tagfolder](https://github.com/vrtmrz/obsidian-tagfolder)

List of all files with all tags in the vault. Instant click to file.

May need a force-reload after installation.


## Themes

### iA Writer

Repo: [mrowa44/obsidian-ia-writer](https://github.com/mrowa44/obsidian-ia-writer)

<!-- The recommended accent colour \(<span title="#18BEEC" style="height: 30px; background-color: #18BEEC; display: inline-block; border-style: solid; border-color: black; color:black; padding-left: 5px; padding-right: 5px;">#18BEEC</span>\) is a bit too light for me, and I used <span title="#4480EF" style="height: 30px; background-color: #4480EF; display: inline-block; border-style: solid; border-color: black; color:white; padding-left: 5px; padding-right: 5px;">#4480EF</span> which has a similar saturation to the default purple colour. -->

The recommended [artisticat1/focus-active-sentence](https://github.com/artisticat1/focus-active-sentence) plugin blinks when scrolling the page, which I found distracting. Instead, I tried [michaellee/stille](https://github.com/michaellee/stille) which turned out to be great.

Unfortunately, the very appealing [artisticat1/nl-syntax-highlighting](https://github.com/artisticat1/nl-syntax-highlighting) only supports English, which is not my primary writing language in Obsidian.

The file tree is very buggy on my setup.


### iB Writer

Repo: [whereiswhere/iB-Writer](https://github.com/whereiswhere/iB-Writer)

Less buggy than iA Writer, but does not respect the accent colour setting.

Some tiny fixes to this theme that I wrote:

{{< highlight-file file="theme-ib.css" lang="css" >}}


### Minimal

Repo: [kepano/obsidian-minimal](https://github.com/kepano/obsidian-minimal)

Changed a lot of CSS classes \(maybe for good but very confusing when writing snippets\). It did not made a huge difference to me compared to default theme with [Hider](#hider), so in the end I went back to that.

Some styles I wrote to make the right sidebar to have the same background colour as the left sidebar:

{{< highlight-file file="theme-minimal.css" lang="css" >}}


## General CSS nippets

> - Style for `text-decoration` will not apply in selection layer.
> - `::selection` does not work for some reason.
{.book-hint .info}

Also see:

- [Obsidian Snippets](https://obsidian-snippets.pages.dev/)
- [Dmytro-Shulha/obsidian-css-snippets](https://github.com/Dmytro-Shulha/obsidian-css-snippets)
- [gitobsidiantutorial / Repositories](https://github.com/gitobsidiantutorial?tab=repositories&type=source)

### Default theme with iA Writer CSS

First 29 lines of [mrowa44/obsidian-ia-writer/theme.css](https://github.com/mrowa44/obsidian-ia-writer/blob/main/theme.css) \(Base64 encoded iA Writer Duo font, too large to include here\), plus:

{{< highlight-file file=`theme-default-ia-trim.css` lang=`css` >}}

### Active pane highlight

Subtle yet effective.

Another choice \(not tested\): [smikula/obsidian-limelight: Spotlight your active pane](https://github.com/smikula/obsidian-limelight)

```css
.mod-active .workspace-tab-header-container {
  border-bottom: 1px solid var(--color-accent);
}
```

### Hide word count in word count plugin

Because I write only want the characters. Only works on desktop, haven't figured out how to do this on mobile \(yet\).

```css
.plugin-word-count .status-bar-item-segment:first-of-type {
  display: none;
  visibility: collapse;
}
```

### Hide new tab button

Old habits die hard.

```css
.workspace-tab-header-new-tab {
  display: none !important;
  visibility: collapse;
}
```

### Internal link indicator

TODO

And: Indicator per URL protocol \(use `:has[href^="message:"]`\)

{{< details "Reference: Default external link indicator" >}}
```css
.external-link {
  color: var(--link-external-color);
  text-decoration-line: var(--link-external-decoration);
  background-position: center right;
  background-repeat: no-repeat;
  background-image: linear-gradient(transparent, transparent), url(public/images/874d8b8….svg);
  background-size: 13px;
  padding-right: 16px;
  background-position-y: 4px;
  cursor: var(--cursor-link);
  filter: var(--link-external-filter);
}
```
{{< /details >}}

### Multi-state checklist

Ref:

- [CSS snippet for multi-state tasks - Help - Obsidian Forum](https://forum.obsidian.md/t/css-snippet-for-multi-state-tasks/50062)
- [Creating tasks that have three possible states instead of two - Help - Obsidian Forum](https://forum.obsidian.md/t/creating-tasks-that-have-three-possible-states-instead-of-two/24105)

I switched to [List Callouts](#list-callouts), but this works very well on v1.4.16:
[Obsidian custom checkbox snippet](https://gist.github.com/OliverBalfour/b87459fd55cf1f5832a2e0996a6f45a0)

### Readable line length adjustment

Ref: [Changes the readable line length in Obsidian Notes. Tested in Obsidian v1.0.0](https://gist.github.com/vii33/f2c3a85b64023cefa9df6420730c7531)

I manually calibrated the following numbers to make each line to have the exact same number of Chinese characters as Notes.app on iPad mini \(same for portrait and landscape\), which is the other environment where I write.  
Tested on Obsidian 1.4.16, with iA Writer Duo font 16px.

```css
body {
  /* target: Note.app on iPad mini 6 */
  --file-line-width: 606px !important;
  /* --file-line-width: 63ch !important; */
}

/* Somehow the numbers are different on iPad  */
@supports (-webkit-touch-callout: none) {
  body {
    --file-line-width: 620px !important;
  }
}
```

### Show close file button at all times

Old habits die hard \(again\).

```css
.workspace .mod-root .workspace-tabs:not(.mod-stacked) .workspace-tab-header:not(.is-active) .workspace-tab-header-inner-close-button {
  display: flex;
}

@media (hover: hover) {
  .workspace .mod-root .workspace-tabs:not(.mod-stacked) .workspace-tab-header:not(.is-active) .workspace-tab-header-inner-close-button:hover {
    background: var(--background-secondary);
  }
}
```

### Sidebar opacity when not in use

{{< highlight-file file="-sidebar.css" lang="css" >}}


## Writing/testing CSS snippets for iOS devices

### Media query

Refs:

- [Media Queries for Standard Devices | CSS-Tricks - CSS-Tricks](https://css-tricks.com/snippets/css/media-queries-for-standard-devices/)
- [iOS Resolution // Display properties of every iPhone, iPad, iPod touch and Apple Watch Apple ever made](https://www.ios-resolution.com/)
- [What Is My Screen Resolution? - WhatIsMyIP.com®](https://www.whatismyip.com/screen-resolution/)
- [css - Get the device width in javascript - Stack Overflow](https://stackoverflow.com/a/48869219)
- [CSS media query to target only iOS devices - Stack Overflow](https://stackoverflow.com/a/47818418/10668706)

<script>
document.addEventListener("DOMContentLoaded", function() {
  var width = window.screen.width;
  var height = window.screen.height;
  var mes = "This device is " + width + " pixels wide x " + height + " pixels high.";
  console.log(mes);
  document.getElementById("screen-resolution").innerText = mes;
});
</script>

<p><span id="screen-resolution">test text</span></p>

> The `device-width` feature is [deprecated](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/device-width). The following code may break at any time.
{.book-hint .warning}

```css
/* Any iOS device */
@supports (-webkit-touch-callout: none) {
  /* ... */ 
}

/* iPad mini 6 */
@media only screen 
  and (min-device-width: 744px) 
  and (max-device-width: 1133px)
  and (-webkit-min-device-pixel-ratio: 2) {
  /* ... */
}

/* iPhone 14 Pro & 15 Pro */
@media only screen 
  and (min-device-width: 393px) 
  and (max-device-width: 852px) 
  and (-webkit-min-device-pixel-ratio: 3) { 
  /* ... */
}
```

### On-device testing

Ref: [[Mobile] IOS : App to work with hidden folder - Share & showcase - Obsidian Forum](https://forum.obsidian.md/t/mobile-ios-app-to-work-with-hidden-folder/25741)

Editors/apps that I have tested:

- [Taio](https://taio.app/): Works. This is my current setup on iPad, with Obsidian in full-screen, and Taio in Slide Over. All changes are reflected in real time.
  1. `Source Code Editing` feature requires the [Pro plan](https://taio.app/#pricing), which has a Lifetime option and I bought it when the app first came out. Please note that it is far more expensive than the other mentioned app called [Textastic](https://www.textasticapp.com/), which I cannot test because it requires iPadOS 16.
  2. Usage: Add folders: {{< menu `Files (folder icon)` `Added Locations` `⊕` `Add Folder` `Pick Obsidian vault` >}}; edit files: {{< menu `Files (folder icon)` `Added locations` `Tap through the folders` `Tap on file to be edited` >}}.
- [a-Shell](https://holzschu.github.io/a-Shell_iOS/): Works.
  1. The included editor is Vim, which is really a hassle to use with on-screen keyboard.
  2. Usage: {{< menu "`pickFolder` to Obsidian vault" "`cd .obsidian/snippets`" "`vim <file>`">}}. \(When opening file that starts with `-` or `+`,like `-cursor.css`, use `vim -- -cursor.css`. [Ref](https://superuser.com/a/1591633)\)
  2. [Brief tutorial](https://forum.obsidian.md/t/mobile-ios-app-to-work-with-hidden-folder/25741#a-shell-tutorial-1).
- [iSH](https://ish.app/): Too lazy to test thoroughly.
  1. I was able to `cd` into my Obsidian vault in iCloud, but the app does not include an editor. [Documentation](https://github.com/ish-app/ish/wiki/FAQ) says a lot of editor should work, including `vim`, `nano`, and `emacs`.
  2. [Brief startup tutorial](https://forum.obsidian.md/t/mobile-ios-app-to-work-with-hidden-folder/25741/2), [official documentation on basic operations](https://github.com/ish-app/ish/wiki/Using-iSH).
- Koder: Does not work. "Open File From Files" feature uses Apple's Files.app, therefore does not show hidden files; and no support for open folders.
- Kodex: Does not work. Same problems as Koder.


## Things to keep an eye on

{{< details "General" >}}
- [Obsidian Plugin Stats](https://obsidian-plugin-stats.vercel.app/)
- [Actions for Obsidian](https://actions.work/actions-for-obsidian) \(As in: Shortcuts.app\)
- [denolehov/obsidian-git: Backup your Obsidian.md vault with git](https://github.com/denolehov/obsidian-git)
- [Obsidian plugin development: cross-platform mobile/desktop testing | Keath Milligan](https://keathmilligan.net/obsidian-plugin-cross-platform-testing)
{{< /details >}}

{{< details "For writing" >}}
- [pourmand1376/obsidian-custom-font: A plugin to set custom font for obsidian](https://github.com/pourmand1376/obsidian-custom-font)
- [Plugins for Writers - Obsidian Hub - Obsidian Publish](https://publish.obsidian.md/hub/02+-+Community+Expansions/02.01+Plugins+by+Category/Plugins+for+Writers)
- [Plugins for Editing Notes - Obsidian Hub - Obsidian Publish](https://publish.obsidian.md/hub/02+-+Community+Expansions/02.01+Plugins+by+Category/Plugins+for+Editing+Notes)
- [Chinese Language Plugins - Obsidian Hub - Obsidian Publish](https://publish.obsidian.md/hub/02+-+Community+Expansions/02.01+Plugins+by+Category/Chinese+Language+Plugins)
- [Japanese Language Plugins - Obsidian Hub - Obsidian Publish](https://publish.obsidian.md/hub/02+-+Community+Expansions/02.01+Plugins+by+Category/Japanese+Language+Plugins)
- [Dictionary and Spellchecking Plugins - Obsidian Hub - Obsidian Publish](https://publish.obsidian.md/hub/02+-+Community+Expansions/02.01+Plugins+by+Category/Dictionary+and+Spellchecking+Plugins)
- [Plugins Designed for Mobile - Obsidian Hub - Obsidian Publish](https://publish.obsidian.md/hub/02+-+Community+Expansions/02.01+Plugins+by+Category/Plugins+Designed+for+Mobile)
- [Outdented marks / Hanging punctuation - Help - Obsidian Forum](https://forum.obsidian.md/t/outdented-marks-hanging-punctuation/34527)
- [holubj/obsidian-dialogue-plugin: Dialogue plugin for Obsidian.md](https://github.com/holubj/obsidian-dialogue-plugin)
{{< /details >}}

{{< details "For note-taking" >}}
- [Vaccarini-Lorenzo/MagicCalendar: An obsidian plugin that exploit a natural language processing engine to find potential events and sync them with iCalendar](https://github.com/Vaccarini-Lorenzo/MagicCalendar)
- [Obsidian Web Clipper — Steph Ango](https://stephanango.com/obsidian-web-clipper) \(Does not work on my Mac for some reason. Firefox v122.0b4.\)
  + [Code](https://gist.github.com/kepano/90c05f162c37cf730abb8ff027987ca3)
- [SilentVoid13/Templater: A template plugin for obsidian](https://github.com/SilentVoid13/Templater)
- [MSzturc/obsidian-advanced-slides: Create markdown-based reveal.js presentations in Obsidian](https://github.com/MSzturc/obsidian-advanced-slides)
- [Phantom1003/obsidian-slide-note](https://github.com/Phantom1003/obsidian-slide-note)
- [The Obsidian Plugins I Actually Use – Curtis McHale](https://curtismchale.ca/2023/02/08/the-obsidian-plugins-i-actually-use/)
- [GitHub - blacksmithgu/obsidian-dataview: A high-performance data index and query language over Markdown files, for https://obsidian.md/.](https://github.com/blacksmithgu/obsidian-dataview)
- [jeweljohnsonj/obsidian_template: A template vault folder for using Obsidian for literature note taking puporses](https://github.com/jeweljohnsonj/obsidian_template)
- [stefanopagliari/bibnotes](https://github.com/stefanopagliari/bibnotes) \(Note: The annotation extraction depends on Zotero's extract annotations from PDF.\)
- [obsidian-tasks-group/obsidian-tasks: Task management for the Obsidian knowledge base.](https://github.com/obsidian-tasks-group/obsidian-tasks)
- [tgrosinger/advanced-tables-obsidian: Improved table navigation, formatting, and manipulation in Obsidian.md](https://github.com/tgrosinger/advanced-tables-obsidian)
{{< /details >}}

{{< details "For reading" >}}
- [KOReader to Obsidian: Export Notes and Highlights](https://hermitage.utsob.me/writings/technical/how-tos/ko-reader-to-obsidian)
- [Edo78/obsidian-koreader-sync: Obsidian.md plugin to sync highlights/notes from koreader](https://github.com/Edo78/obsidian-koreader-sync)
- [NoHeartPen/obsidian-edit-koreader-lua: This is a simple plugin for editing KOReader metadata.epub.lua as a markdown file in Obsidian.](https://github.com/NoHeartPen/obsidian-edit-koreader-lua/tree/master)
- [How I Import Literature Notes into Obsidian | Christian B. B. Houmann](https://bagerbach.com/blog/importing-source-notes-to-obsidian)
{{< /details >}}

{{< details "For Daily Notes" >}}
- [iiz00/obsidian-daily-note-outline: Add a custom view which shows outline of multiple daily notes with headings, links, tags and list items](https://github.com/iiz00/obsidian-daily-note-outline)
- [liamcain/obsidian-periodic-notes: Create/manage your daily, weekly, and monthly notes in Obsidian](https://github.com/liamcain/obsidian-periodic-notes)
- [Kageetai/obsidian-plugin-journal-review: Review your daily notes on their anniversaries, like "what happened today last year"](https://github.com/Kageetai/obsidian-plugin-journal-review)
{{< /details >}}

{{< details "For developing Obsidian" >}}
- [Save console messages to logfile for mobile debugging](https://gist.github.com/liamcain/3f21f1ee820cb30f18050d2f3ad85f3f)
  + [velebit/obsidian-save-console-log: Obsidian plugin that redirects the developer console log to a file](https://github.com/velebit/obsidian-save-console-log)
{{< /details >}}

Remotely related:

- [Visualize whitespaces using css - Stack Overflow](https://stackoverflow.com/a/7901559)
