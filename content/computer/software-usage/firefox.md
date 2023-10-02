---
weight: 400
title: "Firefox"
---

## Tricks

- Hold <kbd>option</kbd>on Mac, <kbd>alt</kbd> on Windows to select any word without opening the link.

## Useful Add-Ons

Moved to [Browser extension](/computer/internet/browser-extension/).

Reference: [All recommended extensions](https://addons.mozilla.org/en-US/firefox/search/?recommended=true&type=extension)

Complete list: [My add-on collection](https://addons.mozilla.org/en-US/firefox/collections/16122644/Default/?page=1&collection_sort=added)


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
- [Most Common User Agents - Tech Blog (wh)](https://techblog.willshouse.com/2012/01/03/most-common-user-agents/)

### `about:config`

Reference: [Firefox: Privacy Related "about:config" Tweaks | PrivacyTools](https://www.privacytools.io/browsers/#about_config)

Ones that I do not follow:

- `dom.event.clipboardevents.enabled`: Setting to `False` will disable [Link Text and Location Copier](https://addons.mozilla.org/en-US/firefox/addon/link-text-and-location-copier/), which I use daily.
- `network.cookie.cookieBehavior`: New versions of Firefox has default `4`, which I think is good enough. Setting to `2` will stop Google from login \(why?\)

### `user.js`

Reference: 

- [GitHub - ghacksuserjs/ghacks-user.js: An ongoing comprehensive user.js template for configuring and hardening Firefox privacy, security and anti-fingerprinting](https://github.com/ghacksuserjs/ghacks-user.js)
- [GitHub - arkenfox/user.js: Firefox privacy, security and anti-tracking: a comprehensive user.js template for configuration and hardening](https://github.com/arkenfox/user.js)


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

### White Outline for Favicon

Solves this problem: [how to fix firefox dark theme favicons issue? : r/firefox](https://www.reddit.com/r/firefox/comments/9mevo2/how_to_fix_firefox_dark_theme_favicons_issue/)

You can see the difference very clearly with the Firefox default theme for macOS. Up is original, down is with my CSS: (with other tweaks)

![Favicon with and without outline](/img/tab_icon_diff.jpg)

In `userChrome.css`:

```css
.tab-icon-image {
  filter: drop-shadow(1px 0 0 white) 
          drop-shadow(-1px 0 0 white) 
          drop-shadow(0 1px 0 white) 
          drop-shadow(0 -1px 0 white) !important;
}
```
