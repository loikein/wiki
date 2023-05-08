---
weight: 300
title: "Bookmarklet"
---
# Bookmarklet

todo: move from [loikein/geeky-bookmarklet-collection: a collection of random bookmarklets](https://github.com/loikein/geeky-bookmarklet-collection)

Refs:

- [illusionfield/bookmarklet-syntax.js](https://gist.github.com/illusionfield/db576c73a103f37e0044)
- [Make Your Own Bookmarklets With jQuery — Smashing Magazine](https://www.smashingmagazine.com/2010/05/make-your-own-bookmarklets-with-jquery/)

Lists:

- [F. David McRitchie's Bookmarklets (JavaScript Favelets)](http://dmcritchie.mvps.org/ie/bookmarklets.htm)
- [Bookmarklets - Paul J. Adam - Web & Mobile Accessibility Consultant in Austin, TX](https://pauljadam.com/bookmarklets.html)
- [17 powerful bookmarklets for your iPhone](https://web.archive.org/web/20120623233011/http://www.lifeclever.com/17-powerful-bookmarklets-for-your-iphone/)

Useful tools:

- [Bookmarkleter](https://chriszarate.github.io/bookmarkleter/)
- [JavaScript Minifier & Compressor | Toptal](https://www.toptal.com/developers/javascript-minifier)

## Dark mode

```js
javascript:void%20function()%7Bconst%20a=document.createElement(%22style%22);a.innerHTML=%22%5Cn%20%20%20%20*,%5Cn%20%20%20%20*:after,%5Cn%20%20%20%20*:before%20%7B%5Cn%20%20%20%20%20%20%20%20color:%20%23D5D6D6%20!important;%5Cn%20%20%20%20%20%20%20%20background-color:%20%23292C2E%20!important;%5Cn%20%20%20%20%7D%5Cn%5Cn%20%20%20%20.tags%20.mask%20%7B%5Cn%20%20%20%20%20%20%20%20background:%20%23292C2E%20!important;%5Cn%20%20%20%20%7D%5Cn%5Cn%20%20%20%20.video%20.mask%20%7B%5Cn%20%20%20%20%20%20%20%20opacity:%200.5%20!important;%5Cn%20%20%20%20%20%20%20%20background:%20%23292C2E%20!important;%5Cn%20%20%20%20%7D%5Cn%5Cn%5Ct.user,%5Cn%20%20%20%20.detailed-note,%5Cn%20%20%20%20.comment%20.box,%5Cn%20%20%20%20.simple-shortcut,%5Cn%20%20%20%20.promo-item%20%7B%5Cn%20%20%20%20%20%20%20%20border-color:%20%23414446%20!important;%5Cn%20%20%20%20%7D%5Cn%22,document.head.appendChild(a);const%20b=document.querySelectorAll(%22*%22);b.forEach(a=%3Ea.classList.add(%22dark%22))%7D();
```

## Dyslexia simulator

Credit: [Dyslexia bookmarklet](https://data.qz.com/2016/dyslexia/)

```js
javascript:(function(){var v='1.12.0';if(window.jQuery===undefined||window.jQuery.fn.jquery<v){var done=false;var script=document.createElement('script');script.src='//code.jquery.com/jquery-'+v+'.min.js';script.onload=script.onreadystatechange=function(){if(!done&&(!this.readyState||this.readyState=='loaded'||this.readyState=='complete')){done=true;dyslexia()}};document.getElementsByTagName('head')[0].appendChild(script)}else{dyslexia()}function dyslexia(){var getTextNodesIn=function(el){return $(el).find(':not(iframe)').addBack().contents().filter(function(){return this.nodeType==3})};var textNodes=getTextNodesIn($('p, h1, h2, h3, h4, span'));function isLetter(char){return/^[\d]$/.test(char)}var wordsInTextNodes=[];for(var i=0;i<textNodes.length;i++){var node=textNodes[i];var words=[];var re=/\w+/g;var match;while((match=re.exec(node.nodeValue))!=null){var word=match[0];var position=match.index;words.push({length:word.length,position:position})}wordsInTextNodes[i]=words}function messUpWords(){for(var i=0;i<textNodes.length;i++){var node=textNodes[i];for(var j=0;j<wordsInTextNodes[i].length;j++){if(Math.random()>1/10){continue}var wordMeta=wordsInTextNodes[i][j];var word=node.nodeValue.slice(wordMeta.position,wordMeta.position+wordMeta.length);var before=node.nodeValue.slice(0,wordMeta.position);var after=node.nodeValue.slice(wordMeta.position+wordMeta.length);node.nodeValue=before+messUpWord(word)+after}}}function messUpWord(word){if(word.length<3){return word}return word[0]+messUpMessyPart(word.slice(1,-1))+word[word.length-1]}function messUpMessyPart(messyPart){if(messyPart.length<2){return messyPart}var a,b;while(!(a<b)){a=getRandomInt(0,messyPart.length-1);b=getRandomInt(0,messyPart.length-1)}return messyPart.slice(0,a)+messyPart[b]+messyPart.slice(a+1,b)+messyPart[a]+messyPart.slice(b+1)}function getRandomInt(min,max){return Math.floor(Math.random()*(max-min+1)+min)}setInterval(messUpWords,50)}})();
```

## Google translate

```js
javascript:var%20t=((window.getSelection&&window.getSelection())%7C%7C(document.getSelection&&document.getSelection())%7C%7C(document.selection&&document.selection.createRange&&document.selection.createRange().text));var%20e=(document.charset%7C%7Cdocument.characterSet);if(t!='')%7Blocation.href='http://translate.google.com/?text='+t+'&hl=zh-CN&langpair=auto%7Czh-CN&tbb=1&ie='+e;%7Delse%7Blocation.href='http://translate.google.com/translate?u='+encodeURIComponent(location.href)+'&hl=zh-CN&langpair=auto%7Czh-CN&tbb=1&ie='+e;%7D;
```

{{< details "已不可用：" >}}
\([credit](http://ctrlq.org/ios/?translate#javascript:location='http://translate.google.com/translate?langpair=auto%7Cen&u='+encodeURIComponent(location))\)

```js
javascript:
location='http://translate.google.com/translate?langpair=auto|en&u='+encodeURIComponent(location)
```

\([credit](https://zhuanlan.zhihu.com/p/36882307)\)

```js
javascript:
var%20t=((window.getSelection&&window.getSelection())||(document.getSelection&&document.getSelection())||(document.selection&&document.selection.createRange&&document.selection.createRange().text));var%20e=(document.charset||document.characterSet);
if(t!=‘’)
{location.href=’http://translate.google.com/?text=‘+t+’&hl=zh-CN&langpair=auto|zh-CN&tbb=1&ie=‘+e;}
else
{location.href=’http://translate.google.com/translate?u=’+encodeURIComponent(location.href)+‘&hl=zh-CN&langpair=auto|zh-CN&tbb=1&ie=’+e;};
```
{{< /details >}}


## Simple notepad in new tab

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

## TOC

Credit: [Electric Development Blog](https://electricdevelopment.blogspot.com/#112221683790577218) \(search for `TOC it!`\)

```js
javascript:var%20fullTOCText%20=%20%22Table%20of%20Contents%22;%20var%20hideBtnText%20=%20%22%5Cu00a0X%5Cu00a0%22;%20var%20RXmatch%20=%20/%5Eh%5B1-4%5D$/i;%20var%20XPmatch%20=%20%22//h1%7C//h2%7C//h3%7C//h4%22;%20var%20resetSelect%20=%20true;%20var%20showHide%20=%20true;%20var%20useCookie%20=%20false;%20var%20addMenuItem%20=%20true;%20function%20f()%20%7B%20if%20(document.getElementsByTagName(%22html%22).length%20&&%20(%20document.getElementsByTagName('h1').length%20%7C%7C%20document.getElementsByTagName('h2').length%20%7C%7C%20document.getElementsByTagName('h3').length%20%7C%7C%20document.getElementsByTagName('h4').length%20)%20&&%20(!useCookie%20%7C%7C%20(useCookie%20&&%20getCookie('autotoc_hide')!='true')))%20%7B%20var%20aHs%20=%20getHTMLHeadings();%20if%20(aHs.length%3E1)%20%7B%20var%20body%20=%20document.getElementsByTagName('body')%5B0%5D;%20body.style.marginBottom%20=%20%2224px%20!important%22;%20addCSS(%20'%23js-toc%20%7Bposition:%20fixed;%20left:%200;%20right:%200;%20top:%20auto;%20bottom:%200;%20width:%20100%25;%20display:%20block;%20border-top:%201px%20solid%20%23777;%20background:%20%23ddd;%20margin:%200;%20padding:%203px;%20z-index:%209999;%20%7D%5Cn'+%20'%23js-toc%20select%20%7B%20font:%208pt%20verdana,%20sans-serif;%20margin:%200;%20margin-left:5px;%20background:%20%23fff;%20color:%20%23000;%20float:%20left;%20padding:%200;%20vertical-align:%20bottom;%7D%5Cn'+%20'%23js-toc%20option%20%7B%20font:%208pt%20verdana,%20sans-serif;%20color:%20%23000;%20%7D%5Cn'+%20'%23js-toc%20.hideBtn%20%7B%20font:%20bold%208pt%20verdana,%20sans-serif%20!important;%20float:%20left;%20margin-left:%202px;%20margin-right:%202px;%20padding:%201px;%20border:%201px%20solid%20%23999;%20background:%20%23e7e7e7;%20%7D%5Cn'+%20'%23js-toc%20.hideBtn%20a%20%7B%20color:%20%23333;%20text-decoration:%20none;%20background:%20transparent;%7D%20%23js-toc%20.hideBtn%20a:hover%20%7B%20color:%20%23333;%20text-decoration:%20none;%20background:%20transparent;%7D'%20);%20var%20toc%20=%20document.createElement(window.opera%7C%7CshowHide?'tocdiv':'div');%20toc.id%20=%20'js-toc';%20if%20(showHide)%20%7B%20var%20hideDiv%20=%20document.createElement('div');%20hideDiv.setAttribute('class','hideBtn');%20var%20hideLink%20=%20document.createElement('a');%20hideLink.setAttribute(%22href%22,%22%23%22);%20hideLink.setAttribute(%22onclick%22,useCookie?%22document.getElementById('js-toc').style.display%20=%20'none';%20document.cookie%20=%20'autotoc_hide=true;%20path=/';%20return%20false;%22:%22document.getElementById('js-toc').style.display%20=%20'none';%22);%20hideLink.appendChild(document.createTextNode(hideBtnText));%20hideDiv.appendChild(hideLink);%20toc.appendChild(hideDiv);%20%7D%20tocSelect%20=%20document.createElement('select');%20tocSelect.setAttribute(%22onchange%22,%20%22if(this.value)%7Bfunction%20flash(rep,delay)%20%7B%20for%20(var%20i=rep;i%3E0;i--)%20%7Bwindow.setTimeout('el.style.background=%5C%22%23ff7%5C%22;',delay*i*2);window.setTimeout('el.style.background=elbg',delay*((i*2)+1));%7D;%7D;%20elid%20=%20this.value;%20el=document.getElementById(elid);%20elbg=el.style.background;%20location.href='%23'+elid;%20flash(5,100);%22+(resetSelect?%22this.selectedIndex=0;%7D%22:%22%7D%22));%20tocSelect.id%20=%20'toc-select';%20tocEmptyOption%20=%20document.createElement('option');%20tocEmptyOption.setAttribute('value','');%20tocEmptyOption.appendChild(document.createTextNode(fullTOCText));%20tocSelect.appendChild(tocEmptyOption);%20toc.appendChild(tocSelect);%20document.body.appendChild(toc);%20for%20(var%20i=0,aH;aH=aHs%5Bi%5D;i++)%20%7B%20if%20(aH.offsetWidth)%20%7B%20op%20=%20document.createElement(%22option%22);%20op.appendChild(document.createTextNode(gs(aH.tagName)+getInnerText(aH).substring(0,100)));%20var%20refID%20=%20aH.id%20?%20aH.id%20:%20aH.tagName+'-'+(i*1+1);%20op.setAttribute(%22value%22,%20refID);%20document.getElementById(%22toc-select%22).appendChild(op);%20aH.id%20=%20refID;%20%7D%20%7D%20%7D%20%7D%20%7D;%20function%20autoTOC_toggleDisplay()%20%7B%20if%20(document.getElementById('js-toc'))%20%7B%20if%20(document.getElementById('js-toc').style.display%20==%20'none')%20%7B%20document.getElementById('js-toc').style.display%20=%20'block';%20if%20(useCookie)%20%7Bdocument.cookie%20=%20'autotoc_hide=;%20path=/';%7D%20%7D%20else%20%7B%20document.getElementById('js-toc').style.display%20=%20'none';%20if%20(useCookie)%20%7Bdocument.cookie%20=%20'autotoc_hide=true;%20path=/';%7D%20%7D;%20%7D%20else%20%7B%20if%20(useCookie)%20%7Bdocument.cookie%20=%20'autotoc_hide=;%20path=/';%7D%20f();%20%7D%20%7D%20function%20getHTMLHeadings()%20%7B%20function%20acceptNode(node)%20%7B%20if%20(node.tagName.match(RXmatch))%20%7B%20if%20(node.value+''!='')%20%7B%20return%20NodeFilter.FILTER_ACCEPT;%20%7D%20%7D%20return%20NodeFilter.FILTER_SKIP;%20%7D%20outArray%20=%20new%20Array();%20if%20(document.evaluate)%20%7B%20var%20nodes%20=%20document.evaluate(XPmatch,%20document,%20null,%20XPathResult.ANY_TYPE,%20null);%20var%20thisHeading%20=%20nodes.iterateNext();%20var%20j%20=%200;%20while%20(thisHeading)%20%7B%20if%20(thisHeading.textContent+''!='')%20%7B%20outArray%5Bj++%5D%20=%20thisHeading;%20%7D%20thisHeading%20=%20nodes.iterateNext();%20%7D%20%7D%20else%20%7B%20var%20els%20=%20document.getElementsByTagName(%22*%22);%20var%20j%20=%200;%20for%20(var%20i=0,el;el=els%5Bi%5D;i++)%20%7B%20if%20(el.tagName.match(RXmatch))%20outArray%5Bj++%5D%20=%20el;%20%7D%20%7D%20return%20outArray;%20%7D%20function%20addCSS(css)%20%7B%20var%20head,%20styleLink;%20head%20=%20document.getElementsByTagName('head')%5B0%5D;%20if%20(!head)%20%7B%20return;%20%7D%20styleLink%20=%20document.createElement('link');%20styleLink.setAttribute('rel','stylesheet');%20styleLink.setAttribute('type','text/css');%20styleLink.setAttribute('href','data:text/css,'+escape(css));%20head.appendChild(styleLink);%20%7D%20function%20gs(s)%7B%20s%20=%20s.toLowerCase();%20var%20ret%20=%20%22%22;%20for%20(var%20i=1;%20i%3C(s.substring(1)*1);i++)%20%7B%20ret%20=%20ret%20+%20%22%5Cu00a0%20%5Cu00a0%20%22;%20%7D%20return%20ret;%20%7D%20function%20getInnerText(el)%20%7B%20var%20s='';%20for%20(var%20i=0,node;%20node=el.childNodes%5Bi%5D;%20i++)%20%7B%20if%20(node.nodeType%20==%201)%20s%20+=%20getInnerText(node);%20else%20if%20(node.nodeType%20==%203)%20s%20+=%20node.nodeValue;%20%7D%20return%20s;%20%7D%20function%20getCookie(cname)%20%7B%20var%20namesep%20=%20cname%20+%20%22=%22;%20var%20ca%20=%20document.cookie.split(';');%20for(var%20i=0,%20c;%20c=ca%5Bi%5D;%20i++)%20%7B%20c%20=%20c.replace(/%5E%5Cs*%7C%5Cs*$/g,%22%22);%20if%20(c.indexOf(namesep)%20==%200)%20%7B%20return%20c.substring(namesep.length,c.length);%20%7D%20%7D%20return%20null;%20%7D%20f();
```
