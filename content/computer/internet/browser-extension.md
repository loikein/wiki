---
weight: 300
title: "Browser extension"
---
# Browser extension

Todo: move from [Firefox ](/computer/software-usage/firefox/) and unify other browsers.

{{< hint info >}}
- If there are multiple similar extensions, I prioritise open source ones.
- Links with specific titles are the closest alternatives that I have used. Empty means I have not <u>found or tried</u> any of them.
- For Edge, [it seems better to use the Edge Add-ons](https://www.reddit.com/r/MicrosoftEdge/comments/hro5v9/microsoft_edge_vs_chrome_extensions/), but I cannot tell.
{{< /hint >}}

## User agents

Not an extension, but probably requires one.

IE: \([credit](https://www.whatismybrowser.com/guides/the-latest-user-agent/internet-explorer)\)

```text
# IE 11
Mozilla/5.0 (Windows NT 6.3; Win64, x64; Trident/7.0; rv:11.0) like Gecko
# IE 7
Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.0)
```

## Essentials

|               | Firefox | Safari \(Mac\) | Safari \(iOS\) | Chrome   | Edge | Explanation |
|---------------|---------|----------------|----------------|----------|------|-------------|
| [uBlock origin](https://ublockorigin.com/) | [Firefox](https://addons.mozilla.org/firefox/addon/ublock-origin/) | [AdGuard for Safari](https://apps.apple.com/app/adguard-for-safari/id1440147259) | [AdGuard](https://apps.apple.com/app/adguard-adblock-privacy/id1047223162) | [Chrome](https://chrome.google.com/webstore/detail/ublock-origin/cjpalhdlnbpafiamejdnhcphjbkeiagm) | [Edge](https://microsoftedge.microsoft.com/addons/detail/ublock-origin/odfafepnkmbhccpbejgmiehpchacaeak) | Ad block & [clean URL](https://www.reddit.com/r/uBlockOrigin/comments/rttrbp/no_longer_any_need_for_the_clearurl_extension/). |
| [Vimium](https://github.com/philc/vimium) | [Firefox](https://addons.mozilla.org/en-GB/firefox/addon/vimium-ff/) | [Vimari](https://apps.apple.com/us/app/vimari/id1480933944?mt=12) |  | [Chrome](https://chrome.google.com/extensions/detail/dbepggeogbaibhgnhhndojpepiihcmeb)   |  | See [Vimium](/computer/software-usage/vimium/). |
| [Open Tabs Next To Current](https://github.com/sblask/webextension-open-tabs-next-to-current) | Deprecated by `browser.tabs.insertAfterCurrent=true` in `about:config` | [(Old) FastScripts workaround](https://daringfireball.net/2018/12/safari_new_tab_next_to_current_tab), [(New) debug menu options](https://www.cultofmac.com/691905/how-to-force-safari-tabs-open-at-end-of-tab-bar/)[^1] |  | [Chrome](https://chrome.google.com/webstore/detail/open-tabs-next-to-current/gmpnnmonpnnmnhpdldahlekfofigiffh) |  | The name says it all. This really should be the default behaviour. |
| [Perfect Home](https://github.com/perfect-things/perfect-home) | [Firefox](https://addons.mozilla.org/firefox/addon/perfect-home/)[^2] |  |  | [Chrome](https://chrome.google.com/webstore/detail/hdekbnedodfockfppllkaaahaibfgcaj) |  | Opera-style new tab / home page. |
|               | Firefox | Safari Mac | Safari iOS | Chrome   | Edge | Explanation |

[^1]: This is the option combination that worked for me:
![](/img/browser_open_tab_safari.png)
[^2]: {{< hint warning >}}Older versions of Firefox used to lack new tab management functionality, so it must be (re)installed after any other extensions that modifies the new tab. This is now an option in Preferences > Home as of v113.0b4.{{< /hint >}}


## Accessibility

|               | Firefox | Safari \(Mac\) | Safari \(iOS\) | Chrome   | Edge | Explanation |
|---------------|---------|----------------|----------------|----------|------|-------------|
| [Smart TOC](https://github.com/FallenMax/smart-toc)| [Firefox](https://addons.mozilla.org/firefox/addon/smart_toc/) | [Table of contents — for Safari](https://apps.apple.com/us/app/table-of-contents-for-safari/id1665115607) | [Table of contents — for Safari](https://apps.apple.com/us/app/table-of-contents-for-safari/id1665115607) | [Chrome](https://chrome.google.com/webstore/detail/smart-toc/lifgeihcfpkmmlfjbailfpfhbahhibba) |   | Add floating table of contents. |
| [HeadingsMap](https://rumoroso.bitbucket.io/) | [Firefox](https://addons.mozilla.org/firefox/addon/headingsmap/) |  |  | [Chrome](https://chrome.google.com/webstore/detail/headingsmap/flbjommegcjonpdmenkdiocclhjacmbi?hl=en) | [Edge](https://microsoftedge.microsoft.com/addons/detail/headingsmap/bokekiiaddinealohkmhjcgfanndmcgo) | Add tree table of contents. Sometimes different with Smart TOC, so I have both. |
| [Display #Anchors](https://github.com/Rob--W/display-anchors) | [Firefox](https://addons.mozilla.org/firefox/addon/display-_anchors) |  |  | [Chrome](https://chrome.google.com/webstore/detail/display-anchors/poahndpaaanbpbeafbkploiobpiiieko) |  | Show all id anchors. |
|               | Firefox | Safari Mac | Safari iOS | Chrome   | Edge | Explanation |


## Privacy

| | Firefox | Safari \(Mac\) | Safari \(iOS\) | Chrome   | Edge | Explanation |
|---------------|---------|----------------|----------------|----------|------|-------------|
| | Firefox | Safari Mac | Safari iOS | Chrome | Edge | Explanation |


## Customise the web

|               | Firefox | Safari \(Mac\) | Safari \(iOS\) | Chrome   | Edge | Explanation |
|---------------|---------|----------------|----------------|----------|------|-------------|
| [Stylus](https://add0n.com/stylus.html) | [Firefox](https://addons.mozilla.org/en-US/firefox/addon/styl-us/) | Safari Mac | Safari iOS | [link](https://chrome.google.com/webstore/detail/stylus/clngdbkpkpeebahjckkjfobafhncgmne) | Edge | See [Custom CSS](/computer/internet/css). |
| [Violentmonkey](https://violentmonkey.github.io/) | [Firefox](https://addons.mozilla.org/firefox/addon/violentmonkey/) | Safari Mac | Safari iOS | [Chrome](https://chrome.google.com/webstore/detail/violent-monkey/jinjaccalgkegednnccohejagnlnfdag) | [Edge](https://microsoftedge.microsoft.com/addons/detail/eeagobfjdenkkddmbclomhiblgggliao) | See [Userscript](/computer/internet/userscript). |
|               | Firefox | Safari Mac | Safari iOS | Chrome | Edge | Explanation |


## Editing & developer

|               | Firefox | Safari \(Mac\) | Safari \(iOS\) | Chrome   | Edge | Explanation |
|---------------|---------|----------------|----------------|----------|------|-------------|
| [Link Text and Location Copier](https://evilnickname.github.io/link-text-location-copier/) | [Firefox](https://addons.mozilla.org/firefox/addon/link-text-and-location-copier/) |  | \(Use [Shortcuts](/computer/software-usage/shortcuts/)\) | [Create Link](https://chrome.google.com/webstore/detail/create-link/gcmghdmnkfdbncmnmlkkglmnnhagajbm)  | Edge | Initially used for making [link boxes](/computer/internet/blogger/#link-box), now used for Markdown and reSt. |
| [Copy Selection as Markdown](https://github.com/0x6b/copy-selection-as-markdown) | [Firefox](https://addons.mozilla.org/firefox/addon/copy-selection-as-markdown/) | Safari Mac | \(Use [Shortcuts](/computer/software-usage/shortcuts/)\) | Chrome   | Edge | Explanation |
| [axe DevTools](https://www.deque.com/axe/devtools/) | [Firefox](https://addons.mozilla.org/firefox/addon/axe-devtools/) |  |  | [Chrome](https://chrome.google.com/webstore/detail/axe-devtools-web-accessib/lhdoppojpmngadmnindnejefpokejbdd) | [Edge](https://microsoftedge.microsoft.com/addons/detail/axe-devtools-web-access/kcenlimkmjjkdfcaleembgmldmnnlfkn) | Check accessibility of websites. |
|               | Firefox | Safari Mac | Safari iOS | Chrome | Edge | Explanation |


## Media

| | Firefox | Safari \(Mac\) | Safari \(iOS\) | Chrome   | Edge | Explanation |
|---------------|---------|----------------|----------------|----------|------|-------------|
| [Ruffle](https://ruffle.rs/) | [Firefox](https://addons.mozilla.org/firefox/addon/ruffle_rs/) | \(See [instruction](https://ruffle.rs/#usage), not tested.\) |  | [Chrome](https://chrome.google.com/webstore/detail/ruffle/donbcfbmhbcapadipfkeojnmajbakjdc) |  | Adobe Flash emulator in Rust. |
| | Firefox | Safari Mac | Safari iOS | Chrome | Edge | Explanation |


## Website-specific

|               | Firefox | Safari \(Mac\) | Safari \(iOS\) | Chrome   | Edge | Explanation |
|---------------|---------|----------------|----------------|----------|------|-------------|
| [Gitako](https://github.com/EnixCoda/Gitako) | [Firefox](https://addons.mozilla.org/firefox/addon/gitako-github-file-tree/) |   |   | [Chrome](https://chrome.google.com/webstore/detail/gitako-github-file-tree/giljefjcheohhamkjphiebfjnlphnokk) | [Edge](https://microsoftedge.microsoft.com/addons/detail/alpoloddcggjhakjemghahlkofjekbca) | File tree for GitHub \(older & better than the official one\), Gitea, Gitee |
| [Augmented Steam](https://augmentedsteam.com/) | [Firefox](https://addons.mozilla.org/firefox/addon/augmented-steam/) | Safari Mac | Safari iOS | [Chrome](https://chrome.google.com/webstore/detail/augmented-steam/dnhpnfgdlenaccegplpojghhmaamnnfp) | [Edge](https://microsoftedge.microsoft.com/addons/detail/augmented-steam/dnpjkgmekpilchdgolfifobohlohlioc) | Add price comparison and other features on Steam. |
| [Keepa](https://keepa.com/) | [Firefox](https://addons.mozilla.org/firefox/addon/keepa/) | [Safari Mac](https://apps.apple.com/app/id1533805339) | [(Standalone app)](https://apps.apple.com/app/keepa-price-tracker/id1518541385) | [Chrome](https://chrome.google.com/webstore/detail/keepa-amazon-price-tracke/neebplgakaahbhdphmkckjjcegoiijjo) | [Edge](https://microsoftedge.microsoft.com/addons/detail/keepa-amazon-price-trac/ejefaeioamebhekmfaclajddbpnnobje) | Add price history graph on Amazon. |
| | Firefox | Safari Mac | Safari iOS | Chrome | Edge | Explanation |


## Lists from Firefox

{{< details "Click to unfold" >}}
### Essentials

- [Auto Tab Discard](https://addons.mozilla.org/en-US/firefox/addon/auto-tab-discard/): Automatically suspend tabs that have not been touched for a while.
- [Awesome RSS](https://addons.mozilla.org/en-US/firefox/addon/awesome-rss/): Show all RSS feeds on current page.
- [Pretty XML](https://addons.mozilla.org/en-US/firefox/addon/pretty-xml/): Human-readable RSS pages.
- [Search by Image](https://addons.mozilla.org/en-US/firefox/addon/search_by_image/)

### Privacy

- [HTTPS Everywhere](https://addons.mozilla.org/en-US/firefox/addon/https-everywhere/)
- [Cookie AutoDelete](https://addons.mozilla.org/en-US/firefox/addon/cookie-autodelete/)
(Replaced [Untrack Me](https://addons.mozilla.org/en-US/firefox/addon/untrack-me/).)
- [User-Agent Switcher and Manager](https://addons.mozilla.org/en-US/firefox/addon/user-agent-string-switcher/): Also works as IE tabs.
- [Terms of Service; Didn’t Read](https://addons.mozilla.org/en-US/firefox/addon/terms-of-service-didnt-read/): Summarises the terms of service of the current website.
- [Google Container](https://addons.mozilla.org/en-US/firefox/addon/google-container/): Separate Google sites (including YouTube) from other history.
- [Decentraleyes](https://addons.mozilla.org/en-US/firefox/addon/decentraleyes/): Stop trackings from CDN \(I don't quite understand, but it looks promising\).

### Others

- [Bionic Reading](https://addons.mozilla.org/en-US/firefox/addon/bionicreading/)
- [Workona](https://addons.mozilla.org/en-US/firefox/addon/workona/): Great tabs & workspaces manager.
- [Shut Up: Comment Blocker](https://addons.mozilla.org/en-US/firefox/addon/shut-up-comment-blocker/): Remove comments from any website.
- [HighlightAll](https://addons.mozilla.org/en-US/firefox/addon/highlightall/): Highlight multiple keywords.
- [Unpinterested!](https://addons.mozilla.org/en-US/firefox/addon/unpinterested/): Remove results from Pinterest in Google image search, or optionally, all searches.  
Disclaimer: I use Pinterest a lot, but it is polluting search results too much I hate it.
- [SearchPreview](https://addons.mozilla.org/en-US/firefox/addon/searchpreview/): Add thumbnails to major search engines' results page \(or as the youngsters say, SERP\).
{{< /details >}}
