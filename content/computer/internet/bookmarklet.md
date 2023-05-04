---
weight: 300
title: "Bookmarklet"
---
# Bookmarklet

todo: move from [loikein/geeky-bookmarklet-collection: a collection of random bookmarklets](https://github.com/loikein/geeky-bookmarklet-collection)

- [browser-tab-notepad](https://gist.github.com/loikein/24692da5ef45242a469dbf316b016c48)


Refs:

- [illusionfield/bookmarklet-syntax.js](https://gist.github.com/illusionfield/db576c73a103f37e0044)

## Dark mode

```js
javascript:void%20function()%7Bconst%20a=document.createElement(%22style%22);a.innerHTML=%22%5Cn%20%20%20%20*,%5Cn%20%20%20%20*:after,%5Cn%20%20%20%20*:before%20%7B%5Cn%20%20%20%20%20%20%20%20color:%20%23D5D6D6%20!important;%5Cn%20%20%20%20%20%20%20%20background-color:%20%23292C2E%20!important;%5Cn%20%20%20%20%7D%5Cn%5Cn%20%20%20%20.tags%20.mask%20%7B%5Cn%20%20%20%20%20%20%20%20background:%20%23292C2E%20!important;%5Cn%20%20%20%20%7D%5Cn%5Cn%20%20%20%20.video%20.mask%20%7B%5Cn%20%20%20%20%20%20%20%20opacity:%200.5%20!important;%5Cn%20%20%20%20%20%20%20%20background:%20%23292C2E%20!important;%5Cn%20%20%20%20%7D%5Cn%5Cn%5Ct.user,%5Cn%20%20%20%20.detailed-note,%5Cn%20%20%20%20.comment%20.box,%5Cn%20%20%20%20.simple-shortcut,%5Cn%20%20%20%20.promo-item%20%7B%5Cn%20%20%20%20%20%20%20%20border-color:%20%23414446%20!important;%5Cn%20%20%20%20%7D%5Cn%22,document.head.appendChild(a);const%20b=document.querySelectorAll(%22*%22);b.forEach(a=%3Ea.classList.add(%22dark%22))%7D();
```

## Google translate

可用：

```js
javascript:
var%20t=((window.getSelection&&window.getSelection())%7C%7C(document.getSelection&&document.getSelection())%7C%7C(document.selection&&document.selection.createRange&&document.selection.createRange().text));
var%20e=(document.charset%7C%7Cdocument.characterSet);if(t!='')%7Blocation.href='http://translate.google.com/?text='+t+'&hl=zh-CN&langpair=auto%7Czh-CN&tbb=1&ie='+e;
%7Delse%7Blocation.href='http://translate.google.com/translate?u='+encodeURIComponent(location.href)+'&hl=zh-CN&langpair=auto%7Czh-CN&tbb=1&ie='+e;%7D;
```

不可用：\([credit](http://ctrlq.org/ios/?translate#javascript:location='http://translate.google.com/translate?langpair=auto%7Cen&u='+encodeURIComponent(location))\)

```js
javascript:
location='http://translate.google.com/translate?langpair=auto|en&u='+encodeURIComponent(location)
```

不可用：\([credit](https://zhuanlan.zhihu.com/p/36882307)\)

```js
javascript:
var%20t=((window.getSelection&&window.getSelection())||(document.getSelection&&document.getSelection())||(document.selection&&document.selection.createRange&&document.selection.createRange().text));var%20e=(document.charset||document.characterSet);
if(t!=‘’)
{location.href=’http://translate.google.com/?text=‘+t+’&hl=zh-CN&langpair=auto|zh-CN&tbb=1&ie=‘+e;}
else
{location.href=’http://translate.google.com/translate?u=’+encodeURIComponent(location.href)+‘&hl=zh-CN&langpair=auto|zh-CN&tbb=1&ie=’+e;};
```

## Simple notepad in tab

{{< hint warning >}}
Only intended for temporary text editing. Once you close it, everything is lost.
{{< /hint >}}

```html
data:text/html,
<html contenteditable
    style="font-size:1.5rem; 
        line-height:1.4; 
        max-width:60rem; 
        margin:0 auto; 
        padding:4rem;" 
    spellcheck="false">
<script>
    document.documentElement.focus();
</script>
<title>Text Editor</title>
```
