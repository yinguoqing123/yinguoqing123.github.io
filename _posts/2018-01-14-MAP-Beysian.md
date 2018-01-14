---
layout: post
title:  最大似然估计和贝叶斯估计
categories: 机器学习
tags:  
mathjax: true
---

* content
{:toc}

频率学派把概率模型中的参数视做一个客观存在的数，固定不变。贝叶斯学派将参数看做随机变量，服从某个分布。





## 问题描述 

已知一堆数据，并且知道这堆数据服从某个带参数的概率分布，（比如服从正态分布，$X \sim N(\mu, \sigma^2)$），现在要由这一堆数据估计参数$\mu$,$\sigma^2$，

令$\theta$表示所有参数，(如$\theta = (\mu, \sigma^2)$)，估计准则是$\arg \max_\theta p(D\|\theta)$

## 最大似然估计

数据集：$D=\{x_1,x_2,...,x_n\}$, $\theta$:表示参数，最大似然估计是使当前数据集出现概率最大的$\theta$值作为估计值

$$
\theta = \arg \max \limits_\theta P(D|\theta) \tag{1}
$$

由贝叶斯公式得：

$$
p(\theta|D)=\frac{p(D|\theta)p(\theta)}{p(D)} \tag{2}
$$

$p(\theta)=1$,所以：

$$
\theta = \arg\max_{\theta}p(D|\theta)\tag{3}
$$

式$(3)$中$p(D\|\theta)$称做似然函数，若$D=\{x_1,x_2,x_3,...,x_n\}$,数据独立，则

$$
p(D|\theta)=\prod_{i=1}^{n}p(x_i|\theta)\tag{4}
$$

实际中为了防止连乘运算导致结果过小，下溢，通常采用对数似然$\log p(D\|\theta)$

## 贝叶斯估计

$\theta$服从一个先验概率，记作$p(\theta)$,需要估计的是知道数据集$D$后，$p(\theta \| D)$的分布，$p(\theta \|D)$称为后验分布,.式(2)中

$$
p(D)=\int_{\theta}p(D|\theta)p(\theta)d\theta\tag{5}
$$

把上式(5)带入(2)中并假设数据独立：

$$
p(\theta|D)=\frac{(\prod_{i=1}^{n}p(x_i|\theta))p(\theta)}{\int_{\theta}
(\prod_{i=1}^{n}p(x_i|\theta))p(\theta)d\theta}\tag{7}
$$

知道后验概率后就可以预测新数据出现的概率：

$$
p(x|D)=\int_{\theta}p(x,\theta|D)d\theta=\int_{\theta}p(x|\theta)p(\theta|D)d\theta\tag{8}
$$

式(8)的积分运算是复杂的，所以可以退而求其次，使用最大后验概率估计。

## 最大后验概率分布

其实就是用使后验概率最大的$\theta$值作为$\theta$的具体值，也变成了点估计，注意到(7)中的分子是一个确定的归一化常数。

$$
\theta = \arg \max_\theta p(\theta| D)=\arg \max_\theta (\prod_{i=1}^{n}p(x_i|\theta))p(\theta)\tag{9}
$$


