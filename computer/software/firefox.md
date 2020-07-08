# Firefox

## User CSS

Ref: [Tutorial: How to create and live-debug userChrome.css : r/FirefoxCSS](https://www.reddit.com/r/FirefoxCSS/comments/73dvty/tutorial_how_to_create_and_livedebug_userchromecss/)

First, access `about:config` in Firefox, and enable `toolkit.legacyUserProfileCustomizations.stylesheets` option (set to `true`).

For macOS, the user profile folder is under: `~/Library/Application Support/Firefox/Profiles/`. If there are multiple profiles, access `about:support` in Firefox to see which is the current profile.

In the profile folder, create a folder and two CSS files with the following names:

```text
.
└── chrome
    ├── userChrome.css
    └── userContent.css
```

### Add White Background for Favicons

Ref: [how to fix firefox dark theme favicons issue? : r/firefox](https://www.reddit.com/r/firefox/comments/9mevo2/how_to_fix_firefox_dark_theme_favicons_issue/)

```css
/* in userChrome.css: */

/* not really necessary: */
/* @namespace url("http://www.mozilla.org/keymaster/gatekeeper/there.is.only.xul"); */

.tab-icon-image { 
  background-color: white !important;
}
```
