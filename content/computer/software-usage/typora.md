---
weight: 400
title: "Typora"
---

> I have stopped using Typora. Proceed at your own risk.
{.book-hint .danger}

## Extra CSS

Under theme folder, create `base.user.css` with:

```css
del {
  text-decoration: none;
  color: red;
}
table{
  counter-reset: tr-number;
}
tr>td:nth-child(1)::before{
  counter-increment: tr-number;
  content: counter(tr-number);
}
```

Ref:

- [[APP] 如何撰寫 Typora 中 markdown 的客製化樣式 ~ PJCHENder 那些沒告訴你的小細節](https://pjchender.blogspot.com/2018/04/app-typora.html)
- [Add Custom CSS](http://support.typora.io/Add-Custom-CSS/)
