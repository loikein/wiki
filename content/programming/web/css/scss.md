---
weight: 100
title: "SCSS"
---

Refs:

- [Nesting in Sass and Less | @mdo](https://markdotto.com/2015/07/20/css-nesting/)
- [Extending CSS With Sass | Ariel Salminen](https://arie.ls/2012/extending-css-with-sass/)


## Dark mode spaghetti code with mixins and functions

That I wrote for [hugo-diary refactorisation](https://github.com/loikein/hugo-theme-diary/issues/2), inspired by [alex-shpak/hugo-book](https://github.com/alex-shpak/hugo-book/blob/master/assets/_defaults.scss#L31-L66).

I have tested [multiple specifications](https://mastodon.social/@loikein/110792322662024781), and turned out this is actually the simplest way.

```scss
// in _defaults.scss:
$color-accent: #037BBA;

@mixin theme-day {
  --back-container-background: #fcfcfc;
  --front-container-background: #ffffff;

  --emphasis-accent: #{darken($color-accent, 10%)};
  --extra-emphasis-accent: #{darken($color-accent, 50%)};
  --color-text: var(--extra-emphasis-accent);

  @if lightness($color-accent) <20% {
    --emphasis-accent: #{$color-accent};
    --extra-emphasis-accent: #{$color-accent};
    --color-text: #{darken($color-accent, 50%)};
  }
}

@mixin theme-night {
  --back-container-background: #212121;
  --front-container-background: #282828;

  --emphasis-accent: #{lighten($color-accent, 10%)};
  --extra-emphasis-accent: #{lighten($color-accent, 30%)};
  --color-text: #{darken(#fff, 10%)};
}

// in _main.scss:
:root {
  @include theme-day;
}

body.night {
  @include theme-night;
}
// …then use var(--variable-names) for the rest of the SCSS files.
```

## Interpolation

### Force to calculate or not to calculate

[css - Force SASS to not calculate the content of a variable? - Stack Overflow](https://stackoverflow.com/questions/50603968/force-sass-to-not-calculate-the-content-of-a-variable)

```scss
$color-accent: #037BBA;

@mixin theme-night {
  @debug lighten($color-accent, 10%);                 // #049cec
  color: lighten($color-accent, 10%);                 // #049cec
  --emphasis-accent: lighten($color-accent, 10%);     // this will not work
  --emphasis-accent: #{lighten($color-accent, 10%)};  // #049cec
}
```

### Mixing SCSS variables and CSS variables

Source: [Sass: Breaking Change: CSS Variable Syntax](https://sass-lang.com/documentation/breaking-changes/css-vars/)

```scss
$accent-color: #fbbc04;

:root {
  // WRONG, will not work in recent Sass versions.
  --accent-color-wrong: $accent-color;

  // RIGHT, will work in all Sass versions.
  --accent-color-right: #{$accent-color};
}
```


## Maps

The following is taken from [hugo-book theme](https://github.com/loikein/hugo-book/), originally authored by [Alex Shpak](https://github.com/alex-shpak).

```scss
$hint-colors: (
  info: #6bf,
  warning: #fd6,
  danger: #f66,
) !default;
```

```scss
// in a loop
// https://github.com/loikein/hugo-book/blob/master/assets/_shortcodes.scss#L96-L105
.markdown .book-hint {
  @each $name, $color in $hint-colors {
    &.#{$name} {
      border-color: $color;
      background-color: rgba($color, 0.1);
    }
  }
}

// one single value
// https://github.com/loikein/hugo-book/blob/master/assets/_custom.scss#L4C1-L6
.markdown details {
  background-color: rgba(map-get($hint-colors, "info"), 0.1);
}
```


## Multi-level counters

Ref: [counters() - CSS: Cascading Style Sheets | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/counters)

The point is to write reset before increment.

```scss
ul{
  counter-reset: index;
  list-style-type: none;

  li {
    counter-increment: item;

    &:before {
      content: counters(item, ".", decimal) ". ";
      float: left;
      margin-inline-end: 4px;
    }
  }
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
