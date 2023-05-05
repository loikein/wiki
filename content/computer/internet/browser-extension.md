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
| [Open Tabs Next To Current](https://github.com/sblask/webextension-open-tabs-next-to-current) | Deprecated by `browser.tabs.insertAfterCurrent` | [(Old) FastScripts workaround](https://daringfireball.net/2018/12/safari_new_tab_next_to_current_tab), [(New) debug menu options](https://www.cultofmac.com/691905/how-to-force-safari-tabs-open-at-end-of-tab-bar/)[^1] |  | [Chrome](https://chrome.google.com/webstore/detail/open-tabs-next-to-current/gmpnnmonpnnmnhpdldahlekfofigiffh) |  | The name says it all. This really should be the default behaviour. |
| [Link Text and Location Copier](https://evilnickname.github.io/link-text-location-copier/) | [Firefox](https://addons.mozilla.org/firefox/addon/link-text-and-location-copier/) | Safari Mac | Safari iOS | [Create Link](https://chrome.google.com/webstore/detail/create-link/gcmghdmnkfdbncmnmlkkglmnnhagajbm)  | Edge | Explanation |
|               | Firefox | Safari Mac | Safari iOS | Chrome   | Edge | Explanation |

[^1]: This is the option combination that worked for me:
![](/img/browser_open_tab_safari.png)

## Privacy

## Customise the web

|               | Firefox | Safari \(Mac\) | Safari \(iOS\) | Chrome   | Edge | Explanation |
|---------------|---------|----------------|----------------|----------|------|-------------|
| [Stylus](https://add0n.com/stylus.html) | [Firefox](https://addons.mozilla.org/en-US/firefox/addon/styl-us/) | Safari Mac | Safari iOS | [link](https://chrome.google.com/webstore/detail/stylus/clngdbkpkpeebahjckkjfobafhncgmne) | Edge | See [Custom CSS](/computer/internet/css) (under construction). |
| [Violentmonkey](https://violentmonkey.github.io/) | [Firefox](https://addons.mozilla.org/firefox/addon/violentmonkey/) | Safari Mac | Safari iOS | [Chrome](https://chrome.google.com/webstore/detail/violent-monkey/jinjaccalgkegednnccohejagnlnfdag) | [Edge](https://microsoftedge.microsoft.com/addons/detail/eeagobfjdenkkddmbclomhiblgggliao) | See [Userscript](/computer/internet/userscript) (under construction). |
|               | Firefox | Safari Mac | Safari iOS | Chrome   | Edge | Explanation |


## Accessibility

|               | Firefox | Safari \(Mac\) | Safari \(iOS\) | Chrome   | Edge | Explanation |
|---------------|---------|----------------|----------------|----------|------|-------------|
| [Smart TOC](https://github.com/FallenMax/smart-toc)| [Firefox](https://addons.mozilla.org/firefox/addon/smart_toc/) | [Table of contents — for Safari](https://apps.apple.com/us/app/table-of-contents-for-safari/id1665115607) | [Table of contents — for Safari](https://apps.apple.com/us/app/table-of-contents-for-safari/id1665115607) | [Chrome](https://chrome.google.com/webstore/detail/smart-toc/lifgeihcfpkmmlfjbailfpfhbahhibba) |   | Add floating table of contents |
|               | Firefox | Safari Mac | Safari iOS | Chrome   | Edge | Explanation |

## Website-specific

|               | Firefox | Safari \(Mac\) | Safari \(iOS\) | Chrome   | Edge | Explanation |
|---------------|---------|----------------|----------------|----------|------|-------------|
| [Gitako](https://github.com/EnixCoda/Gitako) | [Firefox](https://addons.mozilla.org/firefox/addon/gitako-github-file-tree/) |   |   | [Chrome](https://chrome.google.com/webstore/detail/gitako-github-file-tree/giljefjcheohhamkjphiebfjnlphnokk) | [Edge](https://microsoftedge.microsoft.com/addons/detail/alpoloddcggjhakjemghahlkofjekbca) | File tree for GitHub \(older & better than the official one\), Gitea, Gitee |
