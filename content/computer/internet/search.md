---
weight: 100
title: "Search the Internet"
---

Refs:

- [Internet Search Tips · Gwern.net](https://www.gwern.net/Search)
- [dorking (how to find anything on the Internet) - for your information](https://www.alec.fyi/dorking-how-to-find-anything-on-the-internet.html)
- [How to Do Research. v1 | Pabladas de Pablo](https://pabloernesto.github.io/2022/09/07/research-v1.html)


## Google

Refs:

- [Refine web searches - Google Search Help](https://support.google.com/websearch/answer/2466433)
- [60+ Google Search Operators, Tips, Tricks, and Commands (NEW)](https://seosherpa.com/search-operators/)
- [Google Search Operators: The Complete List (44 Advanced Operators)](https://ahrefs.com/blog/google-advanced-search-operators/)
- [Google Search Engine Results API - SerpApi](https://serpapi.com/search-api)
- [Google Url - Documentation - The SERP Spider](https://serp-spider.github.io/documentation/search-engine/google/google-url/)
- [Manage calculator, unit converter & color codes - Google Search Help](https://support.google.com/websearch/answer/3284611)


### Search field operators

{{< hint warning >}}
There must be no space around `:`
{{< /hint >}}

`"word"`
: Must include exact match of `word`

`-word`
: Exclude results with `word`

`intitle:word`
: Search for pages with `word` in title

`-intitle:word`
: Exclude results with `word` in title

`allintitle:word1 word2 word3 ...`
: Search for pages with all words in title

`site:example.com`
: Search within `example.com`

`site:*.example.com -www`
: Search in subdomains of `example.com`

`-site:example.com`
: Exclude results from `example.com`

`inurl:word`
: Search for pages with `word` in URL

`-inurl:word`
: Exclude results with `word` in URL

`allinurl:word1 word2 word3 ...`
: Search for pages with all words in URL

`filetype:pdf`
: Search for only given type of pages \([list of available types](https://developers.google.com/search/docs/crawling-indexing/indexable-file-types)\)

`cache:example.com`
: Return Google cache of `example.com`, if exists


### Search pipes

`( A | B ) C`
: Search for `A C` or `B C`


### Google boxes

`define:word`
: Dictionary box

`map:place`
: Map box

`10lb to kg`
: Unit converter

`color picker`
: Colour picker \& converter

`timer`
: Timer \& stopwatch

### URL parameters

Usage: 

- ``https://www.google.com/search?q=word&param1=value&param2=value&...``

| Param | Values | Meaning | Ref |
|-------|--------|---------|-----|
| `filter` | `0` | Does not filter similar results | [Ref](https://groups.google.com/g/google-search-appliance-help/c/Xm12vbC9xUk) |
| `num` | \<Int\> | Numbers of results per page in SERP | |
| `nfpr` | `1` | Does not auto-correct search query | |
| `safe` | `active` | Turns on safe search (filter adult content) | |
| `hl` | \<language code\> | Shows the SERP UI in specified language | [Ref](https://webapps.stackexchange.com/a/80416) |
| `lr` | `lang_`\<language code\> | Only shows results in specified language | [Ref](https://webapps.stackexchange.com/a/80416) |


<!-- Especially, param `tbs` \& `tbm` -->

### Search trend

Useage:

- `https://trends.google.com/trends/explore?q=word`
- `https://trends.google.com/trends/explore?q=word1,word2,...`


## Entertainment

![xkcd 627 Tech Support Cheat Sheet: 'Hey Megan, it's your father. How do I print out a flowchart?'](https://imgs.xkcd.com/comics/tech_support_cheat_sheet.png)

链接：[xkcd: Tech Support Cheat Sheet](https://xkcd.com/627/)  
翻译：[技術支援流程圖 - xkcd 中文翻譯](https://xkcd.tw/627)
