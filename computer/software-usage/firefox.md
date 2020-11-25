# Firefox

## Tricks

- Hold `option` on Mac, `alt` on Windows to select any word without opening the link.

## Useful Add-Ons

Reference: [All recommended extensions](https://addons.mozilla.org/en-US/firefox/search/?recommended=true&type=extension)

Complete list: [My add-on collection](https://addons.mozilla.org/en-US/firefox/collections/16122644/Default/?page=1&collection_sort=added)

### Basics

- [Auto Tab Discard](https://addons.mozilla.org/en-US/firefox/addon/auto-tab-discard/): Automatically suspend tabs that have not been touched for a while.
- [Perfect Home](https://addons.mozilla.org/en-US/firefox/addon/perfect-home/): Opera style new tab.  
Must be installed after any other extensions that modifies new tab because Firefox only recognise the last extension that does it.
- [Open Tabs Next to Current](https://addons.mozilla.org/en-US/firefox/addon/open-tabs-next-to-current/)
- [Duplicate tab](https://addons.mozilla.org/en-US/firefox/addon/duplicate_tab/): Add a configurable shortcut to duplicate current tab with reserving all history.
- [Awesome RSS](https://addons.mozilla.org/en-US/firefox/addon/awesome-rss/): Show all RSS feeds on current page.
- [Pretty XML](https://addons.mozilla.org/en-US/firefox/addon/pretty-xml/): Human-readable RSS pages.
- [Search by Image](https://addons.mozilla.org/en-US/firefox/addon/search_by_image/)
- [Link Text and Location Copier](https://addons.mozilla.org/en-US/firefox/addon/link-text-and-location-copier/)
- [Copy Selection as Markdown](https://addons.mozilla.org/en-US/firefox/addon/copy-selection-as-markdown/)

### Privacy

- [HTTPS Everywhere](https://addons.mozilla.org/en-US/firefox/addon/https-everywhere/)
- [Cookie AutoDelete](https://addons.mozilla.org/en-US/firefox/addon/cookie-autodelete/)
- [Neat URL](https://addons.mozilla.org/en-US/firefox/addon/neat-url/): Remove tracking information from the URLs like [ClearURLs](https://addons.mozilla.org/en-US/firefox/addon/clearurls/), but can be paused for 3 minutes when (rarely) causes unexpected behaviour.  
(Replaced [Untrack Me](https://addons.mozilla.org/en-US/firefox/addon/untrack-me/).)
- [User-Agent Switcher and Manager](https://addons.mozilla.org/en-US/firefox/addon/user-agent-string-switcher/): Also works as IE tabs.
- [Terms of Service; Didn’t Read](https://addons.mozilla.org/en-US/firefox/addon/terms-of-service-didnt-read/): Summarises the terms of service of the current website.
- [Google Container](https://addons.mozilla.org/en-US/firefox/addon/google-container/): Separate Google sites (including YouTube) from other history.
- [Decentraleyes](https://addons.mozilla.org/en-US/firefox/addon/decentraleyes/): Stop trackings from CDN \(I don't quite understand, but it looks promising\).

### Customise the Web

- [uBlock Origin](https://addons.mozilla.org/en-US/firefox/addon/ublock-origin/)
- [Stylus](https://addons.mozilla.org/en-US/firefox/addon/styl-us/): Custom CSS, see [Custom CSS](../internet/css.md).
- [Tampermonkey](https://addons.mozilla.org/en-US/firefox/addon/tampermonkey/): Custom JavaScript, see [Custom JavaScript](../internet/js.md).
    - See [Userscripts](userscripts.md)

### Accessibility

- [Smart TOC](https://addons.mozilla.org/en-US/firefox/addon/smart_toc/): Add floating table of contents.
- [HeadingsMap](https://addons.mozilla.org/en-US/firefox/addon/headingsmap/): Add table of contents to side of the window including HTML5 landmarks.
- [Gitako - Github file tree](https://addons.mozilla.org/en-US/firefox/addon/gitako-github-file-tree/): File tree for GitHub. \(Replaced [Octotree](https://addons.mozilla.org/en-US/firefox/addon/octotree/).\)
- [axe - Web Accessibility Testing](https://addons.mozilla.org/en-US/firefox/addon/axe-devtools/)

### Others

- [Bionic Reading](https://addons.mozilla.org/en-US/firefox/addon/bionicreading/)
- [Keepa - Amazon Price Tracker](https://addons.mozilla.org/en-US/firefox/addon/keepa/)
- [Augmented Steam](https://addons.mozilla.org/en-US/firefox/addon/enhanced-steam-an-itad-fork/)
- [Workona](https://addons.mozilla.org/en-US/firefox/addon/workona/): Great tabs & workspaces manager.
- [Shut Up: Comment Blocker](https://addons.mozilla.org/en-US/firefox/addon/shut-up-comment-blocker/): Remove comments from any website.
- [HighlightAll](https://addons.mozilla.org/en-US/firefox/addon/highlightall/): Highlight multiple keywords.
- [Unpinterested!](https://addons.mozilla.org/en-US/firefox/addon/unpinterested/): Remove results from Pinterest in Google image search, or optionally, all searches.  
Disclaimer: I use Pinterest a lot, but it is polluting search results too much I hate it.
- [Ruffle \| Flash Player emulator written in the Rust programming language](https://ruffle.rs/#usage)
- [SearchPreview](https://addons.mozilla.org/en-US/firefox/addon/searchpreview/): Add thumbnails to major search engines' results page \(or as the youngsters say, SERP\).

## Vimium-FF

See [Vimium](vimium.md).

## Hidden Configuration Pages

```text
about:about         All hidden pages
about:config        Advanced settings
about:profiles      Profile manager
about:support       Detailed "about this browser"
about:debugging#/runtime/this-firefox
                    Load unsigned extension without changing setting
```

For example, to enable `prefers-reduced-motion` within the browser, add the following pair to `about:config`: \([credit](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-reduced-motion#User_Preferences)\)

```text
ui.prefersReducedMotion        true
```

or add the following to [`user.js`](#better-way-user-js):

```text
// set prefers-reduced-motion
user_pref("ui.prefersReducedMotion", true);
```

## Privacy-Focused Configurations

References:

- [The Firefox Privacy Guide For Dummies! – 12Bytes.org](https://12bytes.org/articles/tech/firefox/the-firefox-privacy-guide-for-dummies)
- [Firefox Privacy: A Guide to Better Browsing](https://blog.privacytools.io/firefox-privacy-an-introduction-to-safe/)
- [Firefox Profilemaker](https://ffprofile.com/)

### Modify `about:config` Directly

Reference: [Firefox: Privacy Related "about:config" Tweaks | PrivacyTools](https://www.privacytools.io/browsers/#about_config)

Ones that I do not follow:

- `dom.event.clipboardevents.enabled`: Setting to `False` will disable [Link Text and Location Copier](https://addons.mozilla.org/en-US/firefox/addon/link-text-and-location-copier/), which I use daily.
- `network.cookie.cookieBehavior`: New versions of Firefox has default `4`, which I think is good enough. Setting to `2` will stop Google from login \(why?\)

### Better Way: `user.js`

Reference: [GitHub - ghacksuserjs/ghacks-user.js: An ongoing comprehensive user.js template for configuring and hardening Firefox privacy, security and anti-fingerprinting](https://github.com/ghacksuserjs/ghacks-user.js)

## Browser CSS

Ref: [Tutorial: How to create and live-debug userChrome.css : r/FirefoxCSS](https://www.reddit.com/r/FirefoxCSS/comments/73dvty/tutorial_how_to_create_and_livedebug_userchromecss/)

First, access `about:config` in Firefox, and enable `toolkit.legacyUserProfileCustomizations.stylesheets` option (set to `true`).

For macOS, the user profile folder is under: `~/Library/Application Support/Firefox/Profiles/`, regardless of Firefox versions. If there are multiple profiles, access `about:support` in Firefox to see which is the current profile (opening this page may cause some Macs to make strange noises, just cope with it).

In the profile folder, create a folder and two CSS files with the following names:

```text
.
└── chrome
    ├── userChrome.css
    └── userContent.css
```

### Add White Outline for Favicons

Ref: [how to fix firefox dark theme favicons issue? : r/firefox](https://www.reddit.com/r/firefox/comments/9mevo2/how_to_fix_firefox_dark_theme_favicons_issue/)

In `userChrome.css`:

```css
/* not really necessary: */
/* @namespace url("http://www.mozilla.org/keymaster/gatekeeper/there.is.only.xul"); */

.tab-icon-image {
  /* background-color: white !important; */
  filter: drop-shadow(1px 0 0 white)
          drop-shadow(-1px 0 0 white)
          drop-shadow(0 1px 0 white)
          drop-shadow(0 -1px 0 white);
}

/* Firefox Quantum userChrome.css tweaks ************************************************/
/* Github: https://github.com/aris-t2/customcssforfx ************************************/
/****************************************************************************************/
/* tab close - always visible*/
#TabsToolbar #tabbrowser-tabs .tabbrowser-tab:not([pinned]) .tab-close-button {
  visibility: visible !important;
  display: block !important;
}
#TabsToolbar #tabbrowser-tabs .tabbrowser-tab:not([pinned])[faviconized="true"] .tab-close-button {
  visibility: collapse !important;
  display: none !important;
}
```
