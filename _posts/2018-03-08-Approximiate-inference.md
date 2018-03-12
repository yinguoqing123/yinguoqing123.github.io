---
layout: post
title:  近似推断
categories: 机器学习
tags:  EM算法  KL散度
mathjax: true
---

* content
{:toc}

当后验分布非常复杂时，为了计算的方便使用简单的分布去近似复杂的积分，如可以将变量进行分组，分组间满足条件独立性，$q(\theta, \mu, \sigma)=q_1(\theta)*q_2(\mu,\sigma)$,且由于
指数族分布的优良性质，常常将$q_1,q_2$假设为指数族分布。





## 拉普拉斯近似

### 一维空间

拉普拉斯近似是用高斯分布近似复杂分布，假设概率分布$p(z) = \frac{1}{Z} f(z)$,Z是概率归一化项，假设近似分布为$q(z)$,

* 求$z_0$，满足$p'(z_0) = 0$
* 高斯分布的log是一个二次函数，所以对$lnf(z)ln⁡f(z)$进行泰勒展开，以$z_0$为中心:
$$\begin{equation}
    \ln f(z) \simeq \ln f(z_0) - \frac{1}{2}A(z - z_0)^2, \; A = - \left. \frac{d^2}{dz^2} \ln f(x)\right|_{z = z_0}
\end{equation}
$$

两边取指数：

$$
\begin{equation}
    f(z) \simeq f(z_0) \exp\left\{- \frac{A}{2}(z - z_0)^2\right\}
\end{equation}
$$

归一化高斯函数：

$$
\begin{equation}
    q(z) = \left(\frac{A}{2\pi}\right)^{1/2} \exp\left\{- \frac{A}{2}(z - z_0)^2\right\}
\end{equation}
$$

### 高维空间

近似分布$p(z)=f(z)/Z$，泰勒展开，以$z_0=\nabla f(z)$ 为中心: 

$$
\begin{equation}
    \ln f(\mathbf{z}) \simeq \ln f(\mathbf{z}_0) - \frac{1}{2}{(\mathbf{z} - \mathbf{z}_0)}^\top A(\mathbf{z} - \mathbf{z}_0), \; A = - \left. \bigtriangledown\bigtriangledown \ln f(\mathbf{z}) \right|_{\mathbf{z} = \mathbf{z}_0}
\end{equation}
$$

两边取指数： 

$$
\begin{equation}
    f(\mathbf{z}) \simeq f(\mathbf{z}_0) \exp\left\{- \frac{1}{2}{(\mathbf{z} - \mathbf{z}_0)}^\top A(\mathbf{z} - \mathbf{z}_0)\right\}
\end{equation}
$$

归一化高斯函数：

$$
\begin{equation}
    q(\mathbf{z}) = \frac{|A|^{1/2}}{(2\pi)^{M/2}} \exp\left\{- \frac{1}{2}{(\mathbf{z} - \mathbf{z}_0)}^\top A(\mathbf{z} - \mathbf{z}_0)\right\} = \mathcal{N}(\mathbf{z}|\mathbf{z}_0, A^{-1})
\end{equation}
$$

## 变分推断

涉及泛函的概念，泛函中函数为自变量，熵就是泛函的一个例子，当概率分布变化时，熵值发生变化。

### $KL(q\|\|p)$

在EM算法中有下式成立：

<div align="center"><img src="/photoes/2018/appro_inf.png" /></div>

注意式中的$Z$包括隐藏变量和参数。

关于最小化$L(q)$的推导，建议看[这里](http://www.orchid.ac.uk/eprints/40/1/fox_vbtut.pdf)。

### $KL(p\|\|q)$

另一种情形是最小化$KL(p\|\|q)$,最优解是边缘分布，边缘分布的求解可以参考图模型中的期望传播框架。

<div align="center"><img src="/photoes/2018/KL_another.png" /></div>

两种散度是不同的，尤其是当原本复杂分布是多峰分布时，第一种的宽度比第二种窄，具体不同可以看PRML第十章中的图。

## 优点

变分贝叶斯推断的优点是可以确定混合模型中的分量个数，而不需要进行交叉验证。

 
