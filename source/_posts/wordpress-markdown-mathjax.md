---
title: wordpress中用Markdown+MathJax插入数学公式
id: 86
categories:
date: 2016-05-15 21:27:01
tags:
  - Markdown
  - math
  - wordpress
---

我用的wordpress模板默认不支持MathJax。可以把下面的代码放到"外观"->"编辑"－>"单个页面(single.php)"或者“主题页脚 (footer.php)”底部就行了。



``` javascript
<!-- mathjax config similar to math.stackexchange -->
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
    jax: ["input/TeX", "output/HTML-CSS"],
    tex2jax: {
        inlineMath: [ ['$', '$'] ],
        displayMath: [ ['$$', '$$']],
        processEscapes: true,
        skipTags: ['script', 'noscript', 'style', 'textarea', 'pre', 'code']
    },
    messageStyle: "none",
    "HTML-CSS": { preferredFont: "TeX", availableFonts: ["STIX","TeX"] }
});
</script>
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>
```

示例：

<pre class="prettyprint">$$
J(\theta) = \frac{1}{2} \sum_{i=1}^m (h_\theta(x^{(i)})-y^{(i)})^2
$$
</pre>

效果如下： $$ J(\theta) = \frac{1}{2} \sum_{i=1}^m (h_\theta(x^{(i)})-y^{(i)})^2 $$

> 参考：[http://blog.kamidox.com/write-math-formula-with-mathjax.html](http://blog.kamidox.com/write-math-formula-with-mathjax.html)