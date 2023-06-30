---
weight: 100
title: "SCSS"
---

## Selectors

### Both parent and children

Credit: [css - How to apply a style to both parent and child in SCSS - Stack Overflow](https://stackoverflow.com/a/42393790/10668706)

```scss
.parent {
  &, .child {
    width: 100%;
  }
}
```
