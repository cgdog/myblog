---
title: wordpress添加社交分享按钮
id: 47
categories:
date: 2016-05-15 17:11:39
tags:
  - wordpress
---

我用的是wordpress2.5.1，只需要在“外观”->“编辑”－>文章页面 (single.php)　的倒数第二行(<?php get_footer(); ?>之前)加上下面这段代码(这是百度的分享代码，效果见本站的分享效果，划动文字或图片，或点击右侧的“分享按钮”)：


``` javascript
<script>window._bd_share_config={"common":{"bdSnsKey":{},"bdText":"","bdMini":"2","bdMiniList":false,"bdPic":"","bdStyle":"0","bdSize":"16"},"slide":{"type":"slide","bdImg":"0","bdPos":"right","bdTop":"100"},"image":{"viewList":["qzone","tsina","tqq","renren","weixin"],"viewText":"分享到：","viewSize":"16"},"selectShare":{"bdContainerClass":null,"bdSelectMiniList":["qzone","tsina","tqq","renren","weixin"]}};with(document)0[(getElementsByTagName('head')[0]||body).appendChild(createElement('script')).src='http://bdimg.share.baidu.com/static/api/js/share.js?v=89860593.js?cdnversion='+~(-new Date()/36e5)];</script>
```

> 官方教程，可以搜索：百度分享代码