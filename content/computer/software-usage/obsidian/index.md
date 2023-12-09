---
weight: 400
title: "Obsidian"
---

> I use Obsidian with macOS 10.15 Catalina, iOS 17, and iPadOS 15.
{.book-hint .info}

## Admin

### Sync between devices

Do not use iCloud WITH git. Pick one.


### Working with multiple vaults

Set a different accent colour for each vault for a more obvious visual reminder.


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
> 2. After launching Obsidian, the plugin takes a few seconds \(I guess depending on the device, and I guess the same on less powerful desktop devices\) to start-up, before which you will see the default cursor;
> 3. During scrolling, the x-cursor will stay at its on-screen position \(as opposed to: in-text position\) for a split second, and may stay there until tapping at a new position. If your main writing device is iOS, this is experience-breaking.
{.book-hint .danger}

If you want to use this solution, disable the previous cursor snippet, and add the following instead. I changed the width and height, and the blinking animation. You cannot write `animation: none` to stop it, because that will leave you with no cursor. Unfortunately I think it is just how this plugin works.

{{< highlight-file file="plugin-ninja-cursor.css" lang="css" >}}


## Plugins \(for peaceful writing\)

### Show Whitespace

Repo: [deathau/cm-show-whitespace-obsidian](https://github.com/deathau/cm-show-whitespace-obsidian)

{{< details "Reference: Core styles of this plugin, obtained from inspection" >}}
Source: [deathau/cm-show-whitespace-obsidian/styles.scss](https://github.com/deathau/cm-show-whitespace-obsidian/blob/main/styles.scss)

{{< highlight-file file="cm-show-whitespace-core.css" lang="css" >}}
{{< /details >}}

Because this plugin has been unmaintained for a while, a patch is needed to make everything look consistent. Add a CSS file with the following contents: \(the `<br>` style came from [here](https://stackoverflow.com/a/64912130)\)

{{< highlight-file file="plugin-whitespace.css" lang="css" >}}

#### Control Characters

Repo: [joethei/obsidian-control-characters](https://github.com/joethei/obsidian-control-characters)

When I was looking for an alternative of [cm-show-whitespace-obsidian](#cm-show-whitespace-obsidian), I found this plugin which also integrates with [mgmeyers/obsidian-style-settings](https://github.com/mgmeyers/obsidian-style-settings) to make customising possible without fiddling with CSS files. However, I did not like the default SVGs, and could not bother with finding new SVGs right now, so I am still using the old plugin.

### Hider

Repo: [kepano/obsidian-hider](https://github.com/kepano/obsidian-hider)

Hide ribbon, vault name, file explorer icons when in writing mode.

### Hover Editor

Repo: [nothingislost/obsidian-hover-editor](https://github.com/nothingislost/obsidian-hover-editor)

Need to turn on the core Page Preview plugin first, or force reload.

Together with `![[]]` embed, and setting hotkeys {{< kbd `option` `↑` >}} and {{< kbd `option` `↓` >}} for swap lines \(credit: [@seviche@kongwoo.icu](https://kongwoo.icu/users/seviche)\) makes an ok block-editing environment[^ulysses].

[^ulysses]: Yes, I am still missing the Ulysses block editing feature.


### Quiet Outline

Repo: [guopenghui/obsidian-quiet-outline](https://github.com/guopenghui/obsidian-quiet-outline)

> This plugin seems to not work on iOS.
{.book-hint .warning}

Use {{< menu `Command palette` `Quiet Outline: Quiet Outline` >}} to activate.

Turning on dragging titles to rearrange document for a pseudo block editing experience.

Some styles I wrote for more obvious current entry highlighting:

{{< highlight-file file="plugin-quiet-outline.css" lang="css" >}}

### Stille

Repo: [michaellee/stille](https://github.com/michaellee/stille)

Click the moon icon in the [Ribbon](https://help.obsidian.md/User+interface/Workspace/Ribbon), or use {{< menu `Command palette` `Stille: Toggle Stille` >}} to activate.


## Plugins \(for aggressive note-taking\)

TBE.

<!--
[smikula/obsidian-limelight: Spotlight your active pane](https://github.com/smikula/obsidian-limelight)
[SilentVoid13/Templater: A template plugin for obsidian](https://github.com/SilentVoid13/Templater)
-->


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

### Readable line length adjustment

Ref: [Changes the readable line length in Obsidian Notes. Tested in Obsidian v1.0.0](https://gist.github.com/vii33/f2c3a85b64023cefa9df6420730c7531)

I manually calibrated the following numbers to make each line to have the exact same number of Chinese characters as Notes.app on iPad mini \(same for portrait and landscape\), which is the other environment where I write.  
Tested on Obsidian 1.4.16, with iA Writer Duo font 16px.

```css
body {
  /* iPad mini 6 */
  /* --file-line-width: 606px !important; */
  --file-line-width: 63ch !important;
  /* iPad mini 5 */
  /* --file-line-width: 586px !important; */
  /* --file-line-width: 61ch !important; */
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

<script>
document.addEventListener("DOMContentLoaded", function() {
  // document.getElementById("screen-resolution").innerText = window.screen.width + " pixels wide X " + window.screen.height + " pixels high";
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

### On-device debugging

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

For writing:

- [Plugins for Writers - Obsidian Hub - Obsidian Publish](https://publish.obsidian.md/hub/02+-+Community+Expansions/02.01+Plugins+by+Category/Plugins+for+Writers)
- [Plugins for Editing Notes - Obsidian Hub - Obsidian Publish](https://publish.obsidian.md/hub/02+-+Community+Expansions/02.01+Plugins+by+Category/Plugins+for+Editing+Notes)
- [Chinese Language Plugins - Obsidian Hub - Obsidian Publish](https://publish.obsidian.md/hub/02+-+Community+Expansions/02.01+Plugins+by+Category/Chinese+Language+Plugins)
- [Japanese Language Plugins - Obsidian Hub - Obsidian Publish](https://publish.obsidian.md/hub/02+-+Community+Expansions/02.01+Plugins+by+Category/Japanese+Language+Plugins)
- [Dictionary and Spellchecking Plugins - Obsidian Hub - Obsidian Publish](https://publish.obsidian.md/hub/02+-+Community+Expansions/02.01+Plugins+by+Category/Dictionary+and+Spellchecking+Plugins)
- [Plugins Designed for Mobile - Obsidian Hub - Obsidian Publish](https://publish.obsidian.md/hub/02+-+Community+Expansions/02.01+Plugins+by+Category/Plugins+Designed+for+Mobile)
- [Outdented marks / Hanging punctuation - Help - Obsidian Forum](https://forum.obsidian.md/t/outdented-marks-hanging-punctuation/34527)

For note-taking:

- [Obsidian Web Clipper — Steph Ango](https://stephanango.com/obsidian-web-clipper)

Remotely related:

- [Visualize whitespaces using css - Stack Overflow](https://stackoverflow.com/a/7901559)
