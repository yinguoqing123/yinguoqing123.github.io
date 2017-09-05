---
layout: post
title:  "凸优化收敛速度与常见迭代终止准则"
categories: 凸优化  
tags:   线性收敛 二阶收敛 终止准则
mathjax: true
---

* content
{:toc}

本文主要介绍凸优化中算法的收敛速度和集中迭代终止准则。





## 收敛速度

### 线性收敛

$\Vert \cdot \Vert$表示2范数

设序列$\{ \mathrm x_k \}$收敛于$\mathrm x^*$,而且


$$
\lim_{k \to \infty} \frac{\Vert \mathrm x_{k+1}-\mathrm x^* \Vert}{\Vert \mathrm x_k-\mathrm x^* \Vert} = \beta 
$$

若$0 \lt \beta \lt 1$,则称序列$\{ \mathrm x_k \}$是线性收敛的，$\beta$为收敛比；若$\beta = 0$，则称序列$\{ \mathrm x_k \}$是超线性收敛的；若$\beta = 1$，则称序列$\{ \mathrm x_k \}$是次线性收敛的。

### p阶收敛

设序列$\{ \mathrm x_k \}$收敛于$\mathrm x^*$,而且对某个实数$p\ge 1$,满足：

$$
\lim_{k \to \infty} \frac{\Vert \mathrm x_{k+1}-\mathrm x^* \Vert}{\Vert \mathrm x_k-\mathrm x^* \Vert^p} = \beta 
$$

则称序列$\{ \mathrm x_k \}$是$p$阶收敛的，从式中可以看出$p$越大，收敛越快，$\beta$越小，收敛越快。

## 迭代终止准则

常见的迭代终止准则有下面几种：

1. $\Vert \mathrm x_{k+1}-\mathrm x_k \Vert \lt \epsilon$(绝对差)或$\frac {\Vert \mathrm x_{k+1}-\mathrm x_k \Vert}　{\Vert \mathrm x_k \Vert} \lt \epsilon$(相对差):表示$x_k$的值基本上已经不变化了

2. $\vert f(\mathrm x_k) - f(\mathrm x) \vert < \epsilon$或$\frac {\vert f(\mathrm x_k) - f(\mathrm x) \vert} {\vert f(\mathrm x_k) \vert}< \epsilon$:表示$f(\mathrm x_k)$的值基本上不变化了

3. $\Vert \nabla f(\mathrm x_k) \Vert = \mathrm g_k \lt \epsilon$:梯度近似为0，函数近似不再下降

4. 以上三种的组合

其中，$\epsilon$是预先给定的充分小的精度实数。 

