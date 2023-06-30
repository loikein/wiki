---
weight: 100
title: "SCSS"
---

## Maps

The following is taken from [hugo-book theme](https://github.com/loikein/hugo-book/tree/master), written by [Alex Shpak](https://github.com/alex-shpak).

```scss
$hint-colors: (
  info: #6bf,
  warning: #fd6,
  danger: #f66,
) !default;
```

```scss
// in a loop
.markdown .book-hint {
@each $name, $color in $hint-colors {
  &.#{$name} {
    border-color: $color;
    background-color: rgba($color, 0.1);
  }
}
}

// one single value
.markdown details {
  background-color: rgba(map-get($hint-colors, "info"), 0.1);
}
```

## Selectors

### Target both parent and children

Credit: [css - How to apply a style to both parent and child in SCSS - Stack Overflow](https://stackoverflow.com/a/42393790/10668706)

```scss
.parent {
  &, .child {
    width: 100%;
  }
}
```
