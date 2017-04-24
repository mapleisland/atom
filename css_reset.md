# CSS Tools - Reset CSS


原文链接[CSS Tools: Reset CSS](http://meyerweb.com/eric/tools/css/reset/)  

重置样式表的目标是减少浏览器在默认行高,标题的边距和字体大小等方面的不一致等.如果你有兴趣，在[2007年5月的帖子](http://meyerweb.com/eric/thoughts/2007/04/18/reset-reasoning/)中讨论了这个背后的一般推理。重置样式经常出现在CSS框架中，原来的"meyerweb reset"发现了进入[Blueprint](http://code.google.com/p/blueprintcss/)等等。  

这里给出的复位样式是非常通用的。例如，没有为`body`元素设置任何默认颜色或背景。我不特别建议你只是在你自己的项目中使用它的未改变的状态。应对其进行调整，编辑，扩展和调整以匹配您的特定复位基线。填写您首选的颜色的页面，链接等。  

换句话说，这是一个起点，而不是一个无触感的自包含的黑盒子。  

如果你想使用我的重置风格，那么随意！它都明确在公共领域（我必须正式说，否则人们问我关于许可）。你可以抓住[文件的副本](http://meyerweb.com/eric/tools/css/reset/reset.css)使用和调整为最适合你。如果你更多的是复制和粘贴类型，或只是想要一个页面预览你会得到什么，这里是。  
``` css
/* http://meyerweb.com/eric/tools/css/reset/ 
   v2.0 | 20110126
   License: none (public domain)
*/

html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed, 
figure, figcaption, footer, header, hgroup, 
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
  margin: 0;
  padding: 0;
  border: 0;
  font-size: 100%;
  font: inherit;
  vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure, 
footer, header, hgroup, menu, nav, section {
  display: block;
}
body {
  line-height: 1;
}
ol, ul {
  list-style: none;
}
blockquote, q {
  quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
  content: '';
  content: none;
}
table {
  border-collapse: collapse;
  border-spacing: 0;
}
```