# JavaScript

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
