---
layout: post
title:  "markdown语法"
categories: markdown
tags:  markdown
author: YGQ
---

* content
{:toc}

简单介绍markdown的语法，具体可以参考[http://www.appinn.com/markdown/#link](http://www.appinn.com/markdown/#link)
 
 
 
 

## 兼容HTML

不在 Markdown 涵盖范围之内的标签，都可以直接在文档里面用 HTML 撰写。不需要额外标注这是 HTML 或是 Markdown；只要直接加标签就可以了。要制约的只有一些 HTML区块元素――比如 <div>、<table>、<pre>、<p> 等标签，必须在前后加上空行与其它内容区隔开，还要求它们的开始标签与结尾标签不能用制表符或空格来缩进。Markdown 的生成器有足够智能，不会在 HTML 区块标签外加上不必要的 <p> 标签。HTML 的区段（行内）标签如 ```<span>、<cite>、<del>``` 可以在 Markdown 的段落、列表或是标题里随意使用。依照个人习惯，甚至可以不用 Markdown 格式，而直接采用 HTML 标签来格式化。举例说明：如果比较喜欢 HTML 的 <a> 或 <img> 标签，可以直接使用这些标签，而不用 Markdown 提供的链接或是图像标签语法。和处在 HTML 区块标签间不同，Markdown 语法在 HTML 区段标签间是有效的

## 区块元素
### 段落与换行
可以使用HTML中的<br/>标签，如果你确实想要依赖 Markdown 来插入 <br /> 标签的话，在插入处先按入两个以上的空格然后回车。
 

 
 
 
