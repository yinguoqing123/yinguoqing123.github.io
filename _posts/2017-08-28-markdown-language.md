---
layout: post
title:  "markdown语法"
categories: Markdown
tags:  Markdown
author: YGQ
---

* content
{:toc}

简单介绍markdown的语法，具体可以参考[http://www.markdown.cn/](http://www.markdown.cn/)。





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
> 
> 1.   这是第一行列表项。
> 2.   这是第二行列表项。
> 
> 给出一些例子代码：
> 
>     return shell_exec("echo $input | $markdown_script");
```

效果：

> 
> 1.   这是第一行列表项。
> 2.   这是第二行列表项。
> 
> 给出一些例子代码：
> 
>     return shell_exec("echo $input | $markdown_script");

区块引用嵌套：

代码：

```
This is the first level of quoting.
>
> > This is nested blockquote.
>
> Back to the first level.
```

效果：

This is the first level of quoting.
>
> > This is nested blockquote.
>
> Back to the first level.

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

代码：
```
*   This is a list item with two paragraphs.

    This is the second paragraph in the list item. You're
only required to indent the first line. Lorem ipsum dolor
sit amet, consectetuer adipiscing elit.

*   Another item in the same list.
```

效果：

*   This is a list item with two paragraphs.

    This is the second paragraph in the list item. You're
only required to indent the first line. Lorem ipsum dolor
sit amet, consectetuer adipiscing elit.

*   Another item in the same list.

列表中放代码区块：

代码：
```
*   一列表项包含一个列表区块：

        <代码写在这>
```

效果：

*   一列表项包含一个列表区块：

        <代码写在这>
		


有序列表示例：

代码：

```
1. java
2. python
3. ruby
```

效果：

1. java
2. python
3. ruby

### 代码区块

要在Markdown中建立代码区块很简单，只要简单地缩进4个空格或是1个制表符就可以。

代码：
```
Here is an example of AppleScript:

    tell application "Foo"
		beep
    end tell
```

效果：

Here is an example of AppleScript:

    tell application "Foo"
		beep
    end tell

### 分割线

代码：

```
下面是一条分割线
************
上面是一条分割线
```

效果：

下面是一条分割线

*************

上面是一条分割线

### 表格，可以使用\|和\-

代码：

```
|月份|收入|支出|
|:---:|:----|:----
|8    | 100 | 200|
|9    | 100|300|
|10   | 200  | 400|
```

效果：

|月份|收入|支出|
|:---:|:----|:----
|8    | 100 | 200|
|9    | 100|300|
|10   | 200  | 400|


## 区段元素

### 网页链接

代码：

```
[百度](http:www.baidu.com "链接到百度")
```

效果：

[百度](http:www.baidu.com "链接到百度")

还有参考式链接

### 强调

代码：

```
*single asterisks*

**single asterisks**
```

效果：

*single asterisks*

**single asterisks**

### 代码

如果要标记一小段行内代码，你可以用反引号把它包起来（`）

代码：

```
Use the `printf()` function.
```

效果：

Use the `printf()` function.

### 图片链接

代码：

```
![网站小图标](/photoes/tubiao.png "小星星")
```

效果：

![网站小图标](/photoes/tubiao.png "小星星")

## 其他

### 反斜杠(转义)

\*literal asterisks\*

还支持一下符号转义

```
\   反斜线
`   反引号
*   星号
_   底线
{}  花括号
[]  方括号
()  括弧
#   井字号
+   加号
-   减号
.   英文句点
!   惊叹号
```

### 自动链接

代码：

```
<http:www.baidu.com>
```

效果：<http:www.baidu.com>

### Markdown扩展

GFM以及在md文件中插入数学公式，[MathJax渲染Latex公式参考博客](http://www.cnblogs.com/linxd/p/4955530.html)

仅输入一个`\`,输出为\;输入`\\`,输出为\\,输出效果一样。
