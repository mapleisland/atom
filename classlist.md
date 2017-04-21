---
title: classlist - 原生js实现addClass,removeClass
categories:
- dom
tags:
- classlist
---

参考文章:[https://developer.mozilla.org/en-US/docs/Web/API/Element/classList](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList)

```javasscript
var el = document.querySelector("#el");
el.classlist.add("bold");
el.classlist.remove("bold");
el.classlist.toggle("bold");
el.classlist.containes("bold");
el.classlist.item();
```