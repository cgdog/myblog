---
title: apache服务器防止域名恶意指向
id: 147
categories:
date: 2016-05-22 11:20:02
tags:
  - apache
  - 域名
---

我刚买的阿里云ECS学生9.9的套餐，服务器软件用的是apache2.4.7。

几天之后，发现网上有一个域名05sh.com，竟然解析到我云主机的IP了，不知道域名的主人出于何种目的。

一个解决方案如下：

相当于单独配置一个VirtualHost，用于接收从恶意域名发来的请求，如：在/etc/apache2/sites-avaliable目录中创建一个err.conf其内容如下：

<pre class="prettyprint">&lt;VirtualHost *:80>
        #注意是*:80，意味着只要不是你设置的域名，都会映射到这个VirtualHost
        ServerAdmin webmaster@localhost
        DocumentRoot /home/xiaolei/www/err
        #在/home/xiaolei/www/err目录下，可以放置当从恶意域名发来请求时，你想要显示的东西，或者什么都不放。
        #此处没有设置ServerName和ServerAlias，以前的apache版本说把ServerName设置为*，但是apache2.4.7会报错，直接省略就行了。
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

&lt;/VirtualHost>
</pre>

然后创建一个软链接:

<pre class="prettyprint">ln -s /etc/apache2/sites-avaliable/err.conf /etc/apache2/sites-enable/err.conf
</pre>

重启apache服务器。

当然，你的域名要对应的VirtualHost要配置好。否则连你自己的域名也会映射到/home/xiaolei/www/err下，这就不好了。

apache2.4.7配置多域名可以参考我的另一篇文章：[apache2.4.7虚拟机配置多域名(其中一个是二级域名)](http://blog.genger.tech/?cat=7)

> 参考：[Apache禁止未经许可的域名访问ECS上的网站](https://help.aliyun.com/knowledge_detail/6715356.html?pos=8#Apache禁止未经许可的域名访问ECS上的网站)