---
title: "JavaScript"
---

> I have not learnt JavaScript properly. Proceed at your own risk.
{.book-hint .warning}

[^1]: test

## Add line breaks for dummies

Ref: [CSS word wrap / line break on underscores in addition to whitespace and hyphens - Stack Overflow](https://stackoverflow.com/a/29497876)

```js
(function() {
  var i, text, code, codes = document.getElementsByTagName('code');
  for (i = 0; i < codes.length;) {
    code = codes[i];
    if (code.parentNode.tagName !== 'PRE' && code.childElementCount === 0) {
      // add line break before
      code.innerHTML = code.innerHTML.replace(/(?<!^|\.|\s)(\.|\(|{|\\|@)/g, '<wbr />\$1');
      // add line break after
      code.innerHTML = code.innerHTML.replace(/(,|})(?!$|\s)/g, '\$1<wbr />');
      // add line breaks around
      code.innerHTML = code.innerHTML.replace(/(?<!^|-|\.|\s)(_|-|=|\/)(?!$|\s)/g, '<wbr />\$1<wbr />');
    }
    i++;
  }
})();
```

## Dialog \(Modal\) on-load

Ref: [Modals Will Never Be The Same - HTML dialog Element](https://blog.webdevsimplified.com/2023-04/html-dialog/)

HTML:

```html
<dialog id="dialog" class="modal">
  <form method="dialog">
    <p>This is a modal which appears immediately at page loading.</p>
    <button type="button" id="dialog--confirm">Confirm</button>
    <button type="button" onclick="location.href='javascript:history.back()'">Go Back</button>
  </form>
<hr />
</dialog>
```

JS:

```js
document.addEventListener('DOMContentLoaded', function(event) {
  const body = document.body;
  body.classList.add("modal-open");
  const dialog = document.getElementById("dialog");
  dialog.show();

  const button = document.getElementById("dialog--confirm");
  button.addEventListener("click", function(event) {
    dialog.close();
    body.classList.remove("modal-open");
  });
});
```

## Rich link copy button

[javascript - How to copy a HyperText link into clipboard without losing the link properties - Stack Overflow](https://stackoverflow.com/questions/53003980/)

## Tooltip

Ref: [Building a fully-accessible help tooltip – Sara Soueidan, inclusive design engineer](https://www.sarasoueidan.com/blog/accessible-tooltips/)

TBA.

<!-- 
## Snippets

Strict equal: (my version)

```js
function strictEquals(a, b){
    if Object.is(a, NaN) || Object.is(b, NaN) {
        return false;
    } else if Object.is(a, -0) && Object.is(b, 0) {
        return true;
    } else if Object.is(a, 0) && Object.is(b, -0) {
        return true;
    } else {
        return Object.is(a, b);
    }
}
```

Strict equal: \([Dan Abramov version](https://gist.github.com/gaearon/08a85a33e3d08f3f2ca25fb17bd9d638)\)

```js
// Like a === b
function strictEquals(a, b) {
  if (Object.is(a, b)) {
    // Same value.
    // Is this NaN?
    if (Object.is(a, NaN)) { // We already know a and b are the same, so it's enough to check a.
      // Special case #1.
      return false;
    } else {
      // They are equal!
      return true;
    }
  } else {
    // Different value.
    // Are these 0 and -0?
    if (
      (Object.is(a, 0) && Object.is(b, -0)) ||
      (Object.is(a, -0) && Object.is(b, 0))
    ) {
      // Special case #2.
      return true;
    } else {
      // They are not equal!
      return false;
    }
  }
}
```
 -->
