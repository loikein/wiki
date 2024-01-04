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

> There must be no space around the `:`
{.book-hint .warning}

`"word"`
: Must include exact match of `word`

`-word`
: Exclude results with `word`

`intitle:word`
: Search for pages with `word` in title

`-intitle:word`
: Exclude results with `word` in title

`after:YYYY-MM-DD`
: Only include results after date

`before:YYYY-MM-DD`
: Only include results before date \(can be combined with `after`\)

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


## Google Programmable Search Engine

URL: [Programmable Search Engine by Google](https://programmablesearchengine.google.com/)

Search across a customised list of websites at the same time.

<!-- [可编程搜索 - 所有搜索引擎](https://programmablesearchengine.google.com/controlpanel/all) -->


## Twitter

Refs: 

- [Search operators | Docs | Twitter Developer Platform Twitter Developer https://developer.twitter.com › docs › rules-and-filtering](https://developer.twitter.com/en/docs/twitter-api/v1/rules-and-filtering/search-operators)
- [Twitter Advanced Search - Use the Twitter search advanced commands](https://www.tweetbinder.com/blog/twitter-advanced-search/)

### Search field operators

> There must be no space around the `:`
{.book-hint .warning}

Example: `keyword filter:follows filter:media -filter:replies since:2021-12-30`  
Searches for `keyword` in anyone the current logged-in account follows, that has media, that is not a reply, that is tweeted after Dec 30 2021.

Note: The search results do not include private accounts, even if you are following them.

| Param | Meaning | Some possible values |
|-------|---|---|
| `filter:` | Only show | `follows`, `media`, `images`, `replies`, `quote`, `retweets`, `links` |
| `from:` | Search in account | Someone's handle (without `@`), case-insensitive |
| `since:` | Search after date | `yyyy-mm-dd` |
| `until:` | Search before date | `yyyy-mm-dd` |


## Entertainment

![xkcd 627 Tech Support Cheat Sheet: 'Hey Megan, it's your father. How do I print out a flowchart?'](https://imgs.xkcd.com/comics/tech_support_cheat_sheet.png)

链接：[xkcd: Tech Support Cheat Sheet](https://xkcd.com/627/)  
翻译：[技術支援流程圖 - xkcd 中文翻譯](https://xkcd.tw/627)
