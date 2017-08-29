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

HTML的元素可以直接在markdown中使用，注意的是在HTML区块内markdown样式无效，在HTML区段内有效


## 区块元素

### 段落与换行

一个 Markdown 段落是由一个或多个连续的文本行组成，它的前后要有一个以上的空行（空行的定义是显示上看起来像是空的，便会被视为空行。比方说，若某一行只包含空格和制表符，则该行也会被视为空行）。普通段落不该用空格或制表符来缩进。

markdown也允许段落内强制换行，可以使用```<br/>```标签

### 标题

markdown支持两种标题的语法

1. 使用====和---
2. 使用#

### 区块引用

使用>，区块引用和其他markdown语法混用示例

代码：

```
> ## 这是一个标题。
> 
> 1.   这是第一行列表项。
> 2.   这是第二行列表项。
> 
> 给出一些例子代码：
> 
>     return shell_exec("echo $input | $markdown_script");
```

效果：

> ## 这是一个标题。
> 
> 1.   这是第一行列表项。
> 2.   这是第二行列表项。
> 
> 给出一些例子代码：
> 
>     return shell_exec("echo $input | $markdown_script");

### 列表

无序列表使用*、+或-作为列表标记,代码：

```
*   Red
*   Green
*   Blue
```

效果：

*   Red
*   Green
*   Blue

有序列表使用




