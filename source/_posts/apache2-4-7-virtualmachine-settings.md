---
title: apache2.4.7虚拟机配置多域名(其中一个是二级域名)
tags:
  - apache
  - 多域名
  - ubuntu
id: 17
categories:
date: 2016-05-15 13:37:25
---

我有一个主域名genger.tech，和一个二级域名blog.genger.tech。想让apache2.4.7服务器，根据域名不同指向不同的站点目录。配置如下：（注意apache2.4.7和以前的本版不太一样。没有httpd.conf文件了）

其中关键点有两个：一是配置ServerName ，二是配置ServerAlias。网上流传的以前版的apache，好像中需要配置ServerName为站点对应域名就行了，但是apache2.4.7，还要配ServerAlias为站点对应域名，否则访问域名时，无法正确指向站点目录。

注意：我这两个VirtualHost的端口都设为80了。

站点一配置文件/etc/apache2/sites-avaliable/my.conf：(这是一个python写的网站)

&lt;VirtualHost *:80&gt;
**ServerName www.genger.tech#关键**
** ServerAlias www.genger.tech#关键，少了这一项，无法正确指向对应的工程目录**
DocumentRoot /home/xiaoyuan/mysite
&lt;Directory /home/xiaoyuan/mysite/mysite&gt;
&lt;Files wsgi.py&gt;
Require all granted
&lt;/Files&gt;
&lt;/Directory&gt;
WSGIScriptAlias / /home/xiaoyuan/mysite/mysite/wsgi.py
Alias /static/ /home/xiaoyuan/mysite/collectedstatic/
&lt;/VirtualHost&gt;
WSGIPythonPath /home/xiaoyuan/mysite

站点二配置文件/etc/apache2/sites-avaliable/wordpress.conf：(这是一个php写的wordpress)

&lt;VirtualHost *:80&gt;

ServerAdmin webmaster@localhost
DocumentRoot /home/blog/www/wordpress
**ServerName blog.gener.tech#关键**
** ServerAlias blog.genger.tech#关键，少了这一项，无法正确指向对应的工程目录**

ErrorLog ${APACHE_LOG_DIR}/error.log
CustomLog ${APACHE_LOG_DIR}/access.log combined
&lt;/VirtualHost&gt;

&nbsp;

&nbsp;