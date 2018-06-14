---
title: 修复wordpress WP_Image_Editor_Imagick 指令注入漏洞
tags:
  - wordpress
id: 39
categories:
date: 2016-05-15 16:57:05
---

收到阿里云的邮件说wordpress存在wordpress WP_Image_Editor_Imagick 指令注入漏洞。

![imagick](http://blog.genger.tech/wp-content/uploads/2016/05/imagick-300x134.png)

在控制台点修复，说要升级到专业版才能修复(我用的是9.87元/月的学生版)。

自己修了。

参考了这篇文章：http://www.skyfox.org/fix-wordpress-editor-choose-injection.html。谢谢。

我用的wordpress2.5.1版，用vim编辑wordpress/wp-includes/media.php 大概在2899行左右有一行代码：



``` javascript
$implementations = apply_filters( 'wp_image_editors', array( 'WP_Image_Editor_Imagick', 'WP_Image_Editor_GD' ) ); 
```

把它改为



``` javascript
$implementations = apply_filters( 'wp_image_editors', array( 'WP_Image_Editor_GD', 'WP_Image_Editor_Imagick' ) );
```

![imagick2](http://blog.genger.tech/wp-content/uploads/2016/05/imagick2-300x20.png) <script>// 
window._bd_share_config={"common":{"bdSnsKey":{},"bdText":"","bdMini":"2","bdMiniList":false,"bdPic":"","bdStyle":"0","bdSize":"16"},"share":{},"image":{"viewList":["qzone","tsina","tqq","renren","weixin"],"viewText":"分享到：","viewSize":"16"},"selectShare":{"bdContainerClass":null,"bdSelectMiniList":["qzone","tsina","tqq","renren","weixin"]}};with(document)0[(getElementsByTagName('head')[0]||body).appendChild(createElement('script')).src='http://bdimg.share.baidu.com/static/api/js/share.js?v=89860593.js?cdnversion='+~(-new Date()/36e5)];
// </script>