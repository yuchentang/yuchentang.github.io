---
sort: 1
---


# 在博客中嵌入XMind思维导图

就像首页提及的那样，之所以产生做这个博客的念头，源头就是在做数据分析复习的思维导图的时候想要有个地方记录下来，另外拥有一方属于自己搭建的天地（虽然暂时是使用的模版，毕竟我对搭建博客一窍不通哈哈哈哈）感觉会不一样。

那么问题就来了，如何在博客里嵌入一个思维导图呢，而不是把它输出为图片之后再嵌入，显然前者是有交互的。

在寻求了多个上传托管思维导图的类似图床的网站未果之后，我回到XMind软件寻求方法。尽管官方和教程都提及了分享到博客的功能，但我却几次更换版本，包括 **XMind 2020**、**XMind 2021**却没有发现。而**XMind 8 Pro**确实拥有，但无奈风格不和我胃口。

后来经过摸索，发现了如何在目前最新版的XMind 2021里实现上传云端并在个人博客里嵌入。首先需要至[*xmind.net*](https://www.xmind.net/)注册账号，而不是[*xmind.cn*](https://www.xmind.cn/)，其账号管理是分开的，后者不具备该功能。然后在XMind软件里登陆该账号，然后文件/File->分享/Share里就会出现博客/Blog的字样。然后将产生的嵌入代码放入网页文章的.md文件即可实现嵌入。产生的嵌入代码形如（其中`******`为对应的编号）：

```html
<iframe src="https://www.xmind.net/embed/******" width="900px" height="540px" frameborder="0" scrolling="no"></iframe>
```

<iframe src="https://www.xmind.net/embed/iR7YAt" width="900px" height="540px" frameborder="0" scrolling="no"></iframe>