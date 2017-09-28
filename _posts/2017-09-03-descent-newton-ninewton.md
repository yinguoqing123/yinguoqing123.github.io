---
layout: post
title:  "无约束凸优化几种常见算法"
categories: 凸优化 
tags:  梯度下降法 Newton法 拟Newton法
mathjax: true
---

* content
{:toc}

本文主要介绍梯度下降法、牛顿法、共轭梯度法和拟牛顿法，并比较各自的收敛性。





## 梯度下降法

每次迭代的搜索方向为负梯度方向，$\mathrm x_{k+1} = \mathrm x_k + \alpha \mathrm g_k^T \mathrm p_k$, 其中$\mathrm p_k = - \mathrm g_k$,梯度下降法式线性收敛的，收敛速度很慢，对局部来说是最速下降方向，但对整体来说，$\mathrm g_{k+1}^T \mathrm p_k = 0$,即前后两次的搜索方向是正交的。 

### 随机梯度下降法和批量梯度下降法

实际中，知道许多样点数据，用最小二乘进行拟合

随机梯度下降法(SGD)：每次迭代求下一个梯度时，随机选一个样本数据代替，计算量少，但易陷入局部最优

批量梯度下降法：类似SGD,选取批量的样本数据

[参考](http://blog.csdn.net/qer_computerscience/article/details/55061521)

[梯度下降算法家族](http://blog.csdn.net/sun_shengyun/article/details/53811882)

## 牛顿法

本质是在一点附近用二次函数去拟合目标函数(泰勒公式)，并找出局部的一个更小点，以此迭代。搜索方向满足$\mathrm G_k \mathrm p_k = - \mathrm g_k$,当方程组有解时，即$\mathrm x_{k+1} = \mathrm x_k - \mathrm G_k^{-1} \mathrm g_k$, $\mathrm G_k $是目标函数的海森矩阵。牛顿法是超线性收敛的，缺点是每次迭代需要计算海森矩阵，计算量非常大。

阻尼牛顿法:

牛顿法的一个缺点是一次迭代后，可能函数值上升了。对此进行改进，对$\mathrm x_k$迭代时，以$\mathrm p_k$为搜索方向进行一维搜索，求步长$\alpha_k$, 且用$\mathrm M_k$代替$\mathrm G_k$。

## 共轭方向法

共轭方向：设$\mathrm G$为n阶正定矩阵，$\mathrm p_1, \cdot \cdot \cdot , \mathrm p_k$为n维向量，如果$\mathrm p_i^T \mathrm G \mathrm p_j = 0(i \neq j )$,则称向量组$\mathrm p_1, \cdot \cdot \cdot , \mathrm p_k$关于$\mathrm G$共轭。 

定理：若共轭，则向量组线性无关。

优点：至多迭代n次，n为$\mathrm x$的维数 。

关键是如何确定共轭方向？？？

### 共轭梯度法(CG)

* 目标函数为正定二次函数:$f(x)=\frac{1}{2} \mathrm x^T \mathrm G \mathrm x + \mathrm b^T \mathrm x +\mathrm c$
* 迭代方向，初始方向为负梯度方向，$\mathrm p_k = -\mathrm g_k + \beta \mathrm p_{k-1}$
* $\beta_{k-1} = \frac {\mathrm g_k^T \mathrm G \mathrm p_{k-1}}{\mathrm p_{k-1}^T \mathrm G \mathrm p_{k-1}}$
* 一维搜索为精确搜索

改进$\beta_{k-1}$，使适用于一般目标函数

### 一般目标函数的共轭梯度法

#### FR共轭梯度法

给定控制误差$\epsilon$

1. 给定初始点$\mathrm x_1, k = 1$
2. 计算$\mathrm g_k = \mathrm g(\mathrm x_k)$
3. 若$\Vert \mathrm g_k \Vert \le \epsilon$,则$\mathrm x^* = \mathrm x_k$,停；否则令$\mathrm p_k=-\mathrm g_k +\beta_{k-1} \mathrm p_{k-1}$,	
<br><br>$
\beta_{k-1}= \begin{cases} \frac{\mathrm g_k^T \mathrm g_k}{\mathrm g_{k-1}^T \mathrm g_{k-1}}, & \text {当$k \gt 1 $时} \\\\ 0, & \text{当$ k $= 1 时} \end{cases}
$ <br><br>
4. 由精确一维搜素确定步长$\alpha_k$满足: $$f(\mathrm x_k + \alpha_k \mathrm p_k) = \min \limits_{\alpha \ge 0} f(\mathrm x_k + \alpha_k \mathrm p_k)$$.
5. 令$\mathrm x_{k+1} = \mathrm x_k + \alpha_k \mathrm p_k$,$k = k + 1$,转步骤2

#### PRP共轭梯度法

PRP公式，$\beta_{k-1}= \begin{cases} \frac{\mathrm g_k^T \mathrm (g_k - g_{k-1})}{\mathrm g_{k-1}^T \mathrm g_{k-1}}, & \text {当$k \gt 1 $时} \\\\ 0, & \text{当$ k $= 1 时} \end{cases}$

### 小结

对于二次函数，两种共轭梯度法等价且是共轭方向法，当对于一般目标函数，海森矩阵不是常数，所产生的方向*不再是共轭方向*，但搜素方向是下降方向。

## 拟牛顿法

最速下降法和阻尼Newton法迭代公式可统一标示为：

$$
\mathrm x_{k+1} = \mathrm x_k - \alpha_k \mathrm H_k \mathrm g_k
$$  

避免求Hessen矩阵，修正公式:

$$
\mathrm H_{k+1} = \mathrm H_k + \mathrm E_k
$$

问题是如何构造修正公式

### DFP算法

修正公式：

$$
\mathrm H_{k+1} = \mathrm H_k - \frac {\mathrm H_k \mathrm y_k \mathrm y_k^T \mathrm H_k}{\mathrm y_k^T \mathrm H_k \mathrm y_k } + \frac {\mathrm s_k \mathrm s_k^T}{\mathrm y_k^T \mathrm s_k}
$$

步骤：

给定控制误差$epsilon$

1. 给定初始点$\mathrm x_0$和初始矩阵$H_0$(一般取单位阵)，计算$\mathrm g_0$，令$k = 0$.
2. 令$\mathrm p_k = - \mathrm H_k \mathrm g_k$
3. 由精确一维搜素确定步长$\alpha_k$满足: $$f(\mathrm x_k + \alpha_k \mathrm p_k) = \min \limits_{\alpha \ge 0} f(\mathrm x_k + \alpha_k \mathrm p_k)$$.
4. 令$\mathrm x_{k+1} = \mathrm x_k + \alpha_k \mathrm p_k$,
5. 若$\Vert \mathrm g_k \Vert \le \epsilon$,则$\mathrm x^* = \mathrm x_k$,停,否则令：<br><br>
$\mathrm s_k = \mathrm x_{k+1} - \mathrm x_k,  \mathrm y_k = \mathrm g_{k+1} -\mathrm g_k$ <br><br>
6. 由DFP修正公式得$\mathrm H_{k+1}$,令$k=k+1$,转步骤2 

优点：超线性收敛，比最速下降法和共轭梯度法有效的多。

### BFGS算法 

修正公式:

$$
\mathrm H_{k+1}=\mathrm H_{k} - \frac{\mathrm H_k \mathrm y_k\mathrm y_k^T \mathrm H_k}{\mathrm y_k^T \mathrm H_k \mathrm y_k}
+ \frac{\mathrm s_k \mathrm s_k^T} {\mathrm y_k^T \mathrm s_k} + \mathrm w_k \mathrm w_k^T
$$

$$
\mathrm w_k =　(\mathrm y_k^T \mathrm H_k \mathrm y_k)^{1/2}\left(\frac {\mathrm s_k} {\mathrm y_k^T \mathrm s_k}-
\frac {\mathrm H_k \mathrm y_k} {\mathrm y_k^T \mathrm H_k \mathrm y_k} \right)
$$

优点：在实际计算中，由于舍入误差和一维搜索的不精确，DFP算法的效率会受到很大影响，但BFGS算法所受影响要小的多，
而采用非精确一维搜索时，DFP算法效率很低，然而BFGS算法任然十分有效。

## Powell方向加速法

前面的方法都需要知道目标函数的一阶、二阶导数，但实际问题的目标函数有时很复杂，其一阶、二阶导数很复杂或难以求得，甚至
有时连目标函数的解析表达式也不知道，只能通过直接测量得到某些点上的函数值，此时，应采用不使用导数的直接法。缺点是收敛速
度慢，计算量随问题的维数的增加而迅速增大。

## 补充

在*Scipy.optimize*模块中有多种算法的实现。

