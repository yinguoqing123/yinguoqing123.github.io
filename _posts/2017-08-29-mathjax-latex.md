---
layout: post
title:  "Latex 数学公式"
categories: Mathjax Latex
tags: Mathjax Latex 数学公式的输入
mathjax: true
---

* content
{:toc}

MathJax是一款运行在浏览器中的开源数学符号渲染引擎，使用MathJax可以方便的在浏览器中显示数学公式，不需要使用图片。目前，MathJax可以解析Latex、MathML和ASCIIMathML的标记语言。可参考[MathJax basic tutorial and quick reference](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference)。





### 排版方式

1. inline,比如`$f(x)=ax+b$`,显示效果$f(x)=ax+b$
2. display，比如:

$$
	f(x)=ax+b
$$	

### 希腊字母

|*名称*|*大写*|*Tex*|*小写*|*Tex*|
|------|------|-----|------|-----|
|alpha|$A$|A|$\alpha$|\alpha|
|beta|$B$|B|$\beta$|\beta|
|gamma|$\Gamma$|\Gamma|$\gamma$|\gamma|
|theta|$\Theta$|\Theta|$\theta$|\theta|
|sigma|$\Sigma$|\Sigma|$\sigma$|\sigma|
|rho|$P$|P|$\rho$|\rho|
|\.\.\.|\.\.\.|\.\.\.|\.\.\.|\.\.\.|

### 上标和下标

上标和下标分别使用^与_，例如x_i^2：$x_i^2$, 或x^{5^6}:$x^{5^6}$

### 括号

1. 小括号与方括号：使用原始的()，[]即可，如(2+3)[4+4]: $(2+3)[4+4]$
2. 大括号：由于大括号{}被用来分组，因此需要使用\\{和\\}表示大括号，也可以使用\\lbrace和\\rbrace来表示。如\{a*b\}:$\{a*b\}$
3. 尖括号：使用\\langle和\\rangle表示左尖括号和右尖括号。如\\langle x \\rangle : $\\langle x \\rangle$
4. 上取整：使用\\lceil和\\rceil表示。如\\lceil x \\rceil：$\\lceil x \\rceil$
5. 下取整：使用\\lfloor和\\rfloor表示。如\\lfloor x \\rfloor：$\\lfloor x \\rfloor$
6. 不可见括号：使用\.表示

需要注意的是，*原始符号*并不会随着公式大小缩放，可以使用\\left(\.\.\.\\right)来自适应地调整括号大小。如下

$$
\lbrace\sum_{i=0}^{100} i^2 = \frac{(n^2+n)(2n+2)}{6}\rbrace\tag{1.1}
$$

$$
\left\lbrace\sum_{i=0}^0 i^2 = \frac{(n^2+n)(2n+2)}{6}\right\rbrace\tag{1.2}
$$

### 求和和积分

1. \\sum用来表示求和符号，其下标表示求和下限，上标表示上限。如\\sum_1^n:$\\sum_1^n$ 。

2. \\int用来表示积分符号，同样地，其上下标表示积分的上下限。如\\int_1^\\infty: $\\int_1^\\infty$。

3. 与此类似的符号还有：\\prod:$\\prod$ , \\bigcup: $\\bigcup$ , \\bigcap:$\\bigcap$, \\iint:$\iint$。

### 分式和根式

* 分式 
	* 第一种，使用\\frac {ab}{cd}:$\\frac {ab}{cd}$
	* 第二种，使用\\over
* 根式使用\\sqrt,如\\sqrt{7a}：$\\sqrt[8]{7a}$

### 字体

1. 使用\\mathbb或\\Bbb显示黑板粗体字，此字体经常用来表示实数、整数、有理数、复数，如\\mathbb{CHNQRZ}:$\\mathbb{CHNQRZ}$
2. 使用\mathbf显示黑体字,\\mathbf{ABCDEFGHIJKLMNOPQRSTUVWXYZ}
$$
\mathbf{ABCDEFGHIJKLMNOPQRSTUVWXYZ}
$$
3. 使用\mathscr显示手写体,\\mathscr{ABCDEFGHIJKLMNOPQRSTUVWXYZ}
$$
\mathscr{ABCDEFGHIJKLMNOPQRSTUVWXYZ}
$$

###  特殊函数和符号

1. 常见的三角函数，如$\\sin (7x)$ ,$\\arctan_x$ ,$\\lim_{1\\to\\infty}$
2. 比较运算符：$\\lt$,$\\le$,$\\gt$,$\\ge$,可以在这些运算符前面加上\\not,如\\not\\lt:$\\not\\lt$
3. \\times ,\\div, \\pm, \\mp表示：$\\times$ ,$\\div$, $\\pm$, $\\mp$,\\cdot表示居中的点，$x \\cdot y $ ,\\* 表示星号，$\*$
4. 集合关系运算符
5. 箭头
6. 逻辑运算符
7. \\approx, \\sim, \\cong,\\equiv ,\\prec 
8. \\infty ,\\aleph_o ,\\nabla ,\\partial, \\Im ,\\Re,$-\\infty $
9.  模运算 \\pmode , 如 a \\equiv b \\pmod n:$a \\equiv b \\pmod n$
10. \\ldots与\\cdots，其区别是dots的位置不同，ldots位置稍低，cdots位置居中
11. 一些希腊字母具有变体形式

使用[Detexify](http://detexify.kirelabs.org/classify.html)，你可以在网页上画出符号，Detexify会给出相似的符号及其代码。这是一个方便的功能，但是不能保证它给出的符号可以在MathJax中使用，你可以参考supported-latex-commands确定MathJax是否支持此符号

### 空间(改变符号间隙)

通常MathJax通过内部策略自己管理公式内部的空间，因此a\.\.\.b与a\.\.\.\.\.\.b( \. 表示空格)都会显示为ab。可以通过在ab间加入\\,增加些许间隙，\\;增加较宽间隙，\\quad与\\qquad会增加更大的间隙，如 

### 顶部符号

对于单字符，\\hat :  $\\hat x$;

对于多字符，\\widehat $\widehat :x$

类似的还有 \\overline , \\vec , \\overrightarrow , \\dot , \\ddot : $\\overline xyz$ ,$ \\vec a$, $\\overrightarrow x$,$\\dot x$,$\\ddot x$

基础部分就是这些。需要注意的是一些MathJax使用的特殊字符，可以使用\\转义为原来的含义，如\\_表示下划线。

### 表格

使用```$$\begin{array}{列样式}...\end{array}$$```这样的形式来创建表格，列样式可以是clr表示居中，左，右对齐，还可以使用\|表示一条竖线。表格中各行使用\\\分隔，各列使用&分隔，使用\\hline在本行前加入一条直线,例如：

$$
\begin{array}{c|lcr} n & \text{Left} & \text{Center} & \text{Right} \\ \hline 1 & 0.24 & 1 & 125 \\ 2 & -1 & 189 & -8 \\ 3 & -20 & 2000 & 1+10i \\ \end{array}
$$

一个复杂的例子如下

$$
\begin{array}{c}\begin{array}{cc}\begin{array}{c|cccc} \text{min} & 0 & 1 & 2 &3 \\ \hline 0 & 0 & 0 & 0 & 0 \\ 1 & 0 & 1 & 1 & 1 \\ 2 & 0 & 1 & 2 & 2 \\ 3 & 0 & 1 & 2 & 3  \end{array} & \begin{array}{c|cccc} \text{max} & 0 & 1 & 2 & 3 \\ \hline 0 & 0 & 1 & 2 & 3 \\ 1 & 1 & 1 & 2 & 3 \\ 2 & 2 & 2 & 2 & 3 \\ 3 & 3 & 3 & 3 & 3 \end{array} \end{array} \\ \begin{array}{c|cccc} \Delta & 0 & 1 & 2 & 3 \\ \hline 0 & 0 & 1 & 2 & 3 \\ 1 & 1 & 0 & 1 & 2 \\ 2 & 2 & 1 & 0 & 1 \\ 3 & 3 & 2 & 1 & 0 \end{array}\end{array}
$$

### 矩阵

使用```$$\begin{matrix}...\end{matrix}$$```来表示矩阵，在\begin与\end之间加入矩阵的元素即可。矩阵的行之间用\\\\分隔，列之间用&分隔。例如：

$$
\begin{matrix} 1 & x & x^2 \\ 1 & y & y^2 \\ 1 & z & z^2 \end{matrix}
$$

#### 加括号

如果要对矩阵加括号，可以像上文中提到的那样，使用\left与\right配合表示括号符号。也可以使用特殊的matrix，即替换```\begin{matrix}...\end{matrix}```中的matrix为pmatrix , bmatrix , Bmatrix , vmatrix , Vmatrix.$\begin{pmatrix} 1 & 2 \\ 3 & 4 \\ \end{pmatrix}$ , $\begin{bmatrix} 1 & 2 \\ 3 & 4 \\ \end{bmatrix}$,$\begin{Bmatrix} 1 & 2 \\ 3 & 4 \\ \end{Bmatrix}$,$\begin{vmatrix} 1 & 2 \\  3 & 4 \\ \end{vmatrix}$,$\begin{Vmatrix} 1 & 2 \\ 3 & 4 \\ \end{Vmatrix}$



#### 省略元素

可以使用\cdots:$\cdots$,\ddots : $\ddots$,\vdots :$\ddots$ 来省略矩阵中的元素，如：

$$
\begin{pmatrix} 1 & a_1 & a_1^2 & \cdots & a_1^n \\ 1 & a_2 & a_2^2 & \cdots & a_2^n \\ \vdots & \vdots & \vdots & \ddots & \vdots \\ 1 & a_m & a_m^2 & \cdots & a_m^n \end{pmatrix}
$$

#### 增广矩阵

增广矩阵需要使用前面的array来实现，如 ```$$ \left[ \begin{array}{cc|c} 1 & 2 & 3 \\ 4 & 5 & 6 \end{array} \right] $$ ```结果:

$$
\left[ \begin{array}{cc|c} 1 & 2 & 3 \\ 4 & 5 & 6 \end{array} \right]
$$

### 对齐的公式

有时候可能需要一系列的公式中等号对齐，如：

$$
\begin{align} \sqrt{37} & = \sqrt{\frac{73^2-1}{12^2}} \\ & = \sqrt{\frac{73^2}{12^2} \cdot \frac{73^2-1}{73^2}} \\ & = \frac{73}{12} \sqrt{1 - \frac{1}{73^2}} \\ & \approx \frac{73}{12} \left( 1 - \frac{1}{2 \cdot 73^2} \right) \end{align}
$$

这时候需要使用形如```\begin{align}...\end{align}```的格式，其中需要使用&来指示需要对齐的位置.

### 分类表达式

定义函数的时候经常需要分情况给出表达式，可使用```\begin{cases}...\end{cases}```。其中，使用\来分类，使用&指示需要对齐的位置。如：

$$
f(n) = \begin{cases} n/2, & \text{if $n$ is even} \\ 3n+1, & \text{if $n$ is odd} \end{cases}
$$

$$
\left. \begin{array}{l} \text{if $n$ is even:} & n/2 \\ \text{if $n$ is odd:} & 3n+1 \end{array} \right\} = f(n)
$$

如果需要让分类之间的垂直间隔变大，可以使用\[2ex]代替\来分隔不同情况。（3ex, 4ex也可以使用，1ex相当于原始距离）

### 注意事项

在使用LaTex公式时，有一些不会影响公式正确性，但会使其看上去很糟糕的问题。

#### 不要在指数或者积分中使用\frac

在指数或者基本表达式中使用\frac会使表达式看起来不清晰，因此在专业的数学排版中很少被使用。应该使用一个水平的/来代替，效果如下：

$$
\begin{array}{cc} \mathrm{Bad} & \mathrm{Better} \\ \hline \\ e^{i\frac{\pi}{2}} \quad e^{\frac{i\pi}{2}} & e^{i\pi/2} \\ \int_{-\frac{\pi}{2}}^{\frac{\pi}{2}} \sin x \, dx & \int_{-\pi/2}^{\pi/2} \sin x \, dx \\ \end{array}
$$

#### 使用\mid代替\|作为分隔符

符号\|作为分隔符时有排版空间大小的问题，应该使用\mid代替，效果如下:

$$
\begin{array}{cc} \mathrm{Bad} & \mathrm{Better} \\ \hline \\ \{x | x^2 \in \Bbb Z\} & \{x \mid x^2 \in \Bbb Z \} \end{array}
$$

#### 多重积分

对于多重积分，不要使用\int\int此类的表达，应该使用\iint \iiint等特殊形式，效果如下：

$$
\begin{array}{cc} \mathrm{Bad} & \mathrm{Better} \\ \hline \\ \iiint_V f(x) dz dy dx & \iiint_V f(x) \, dz \, dy \, dx \end{array}
$$

#### 连分数

书写连分数表达式时，请使用\cfrac代替\frac或者\over，两者效果对比如下：

$$
x = a_0+\cfrac{1^2}{a_1+\cfrac{2^2}{a_2+\cfrac{3^2}{a_3+\cfrac{4^2}{a_4+\cdots}}}} \tag{\cfrac}
$$

$$
x = a_0+\frac{1^2}{a_1+\frac{2^2}{a_2+\frac{3^2}{a_3+\frac{4^2}{a_4+\cdots}}}} \tag{\frac}
$$

#### 方程组

使用\begin{array}...\end{array}与\left{...与\right.配合表示方程组，如：

$$
\left\{ \begin{array}{c} a_1x+b_1y+c_1z=d_1 \\ a_2x+b_2y+c_2z=d_2 \\ a_3x+b_3y+c_3z=d3 \end{array} \right.
$$

对齐方程组中的＝号，可以使用```\begin{aligned}...\end{aligned}```，如：

$$
\left\{ \begin{aligned} a_1x+b_1y+c_1z & = d_1+e_1 \\ a_2x+b_2y & = d_2 \\ a_3x+b_3y+c_3z & = d_3 \end{aligned} \right.
$$

### 公式标记和引用

使用`\tag{yourtat}`来标记公式，如果想在之后引用该公式，则还需要加上`\label{yourlabel}`在`\tag`之后，如：

$$
a:= x^2-y^3 \tag{*}\label{*}
$$

为了引用公式，可以使用`\eqref{rlabel}`，如：

$$
a+y^3 \stackrel{\eqref{*}}=x^2
$$

可以看到，通过超链接可以跳转到被引用公式的位置。

### 补充

向量、矩阵：\mathrm{x, y}：$\mathrm{x, y}$ 

实值x：$x$

偏导数：\partial f:$\partial f$

双竖线：\Vert $\Vert$,\parallel:$\parallel$








