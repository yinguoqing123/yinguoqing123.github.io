---
layout: post
title:  解决github中下载项目慢的原因
categories: github

mathjax: true
---

* content
{:toc}

github下载慢是因为国内被墙了，可以跳过域名解析，将ip地址与域名绑定。登录[http://github.global.ssl.fastly.net.ipaddress.com/#ipinfo](http://github.global.ssl.fastly.net.ipaddress.com/#ipinfo),可以查询IP地址，再在C:\Windows\System32\drivers\etc文件中绑定
IP地址和域名映射即可。在cmd命令行中输入ipconfig /flushdns 刷新dns缓存即可。