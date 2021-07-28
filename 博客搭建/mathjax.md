---
sort: 2
---


# 在博客中渲染 $\LaTeX$ 公式

没想到在**Markdown**中写的风生水起的$\LaTeX$公式，网页没法渲染。经过一些查询，决定加载**mathjax**这个渲染器。

当然，经过对比发现了该博客的最新框架中涵盖了**mathjax.liquid**文件，但将其内容改成了如下，因为其原始版本无法渲染行内公式，即以`$...$`形式存在的公式。

```html
<script type="text/x-mathjax-config">MathJax.Hub.Config({tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}});</script>
<script type="text/javascript" async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-MML-AM_CHTML"></script>
```
其中之所以选择了cdnjs的网址，而不是网上众多教程所使用的，原因可见[Link](https://www.mathjax.org/cdn-shutting-down/).