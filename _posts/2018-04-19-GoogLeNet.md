---
layout: post
title:  GoogLeNet
categories: 经典CNN
tags:  CV
mathjax: true
---

* content
{:toc}

GoogLeNet和VGG是2014年imagenet双雄，共同点是深度越来越深。





## VGG

vgg的创新点是两层3*3卷积的感受野和5*5卷积的感受野相同，同时非线性拟合能力更强，因为多了一层非线性激活函数。

## GoogLeNet

基础是Inception,从Inception v1发展到Inception v4

1*1卷积降维，两个3*3等价与一个5*5，1*3和3*1等价与3*3

在大量研究的基础上，*用密集的子阵计算替代稀疏的子阵计算，*提出了Inception。1*1卷积的作用是降维，减少参数数量。

> Their main result states that if the probability distribution of the dataset is
representable by a large, very sparse deep neural network,
then the optimal network topology can be constructed layer
after layer by analyzing the correlation statistics of the preceding
layer activations and clustering neurons with highly
correlated outputs. Although the strict mathematical proof
requires very strong conditions, the fact that this statement

如果数据分布可以由深的、稀疏连接的神经网络表示，那么该网络结构可以这样构建，分析当前层输出值的统计相关性，并将
高度相关的神经元聚为一类，与前一层构成一个稀疏连接，一层一层的构建。neurons that fire together, wire together(一起放电的，连接在一起)，通俗讲对同一特征起反应的神经元的功能是类似的。(不知道理解的对不对，有需要的话可以查看相关资料。)GoogLeNet的结构创新也是
基于别人的理论研究。

<div align="center"><img src="/photoes/2018/inception.png" /></div>

<div align="center"><img src="/photoes/2018/googlenet2.png" /></div>

<div align="center"><img src="/photoes/2018/googlenet1.png" /></div>

优化函数中添加了加权的两个辅助损失，加权值为0.3，便于缓解层数过深造成的梯度消失。全连接层是便于迁移到其他任务中微调，本身
在训练中不存在。随着层数的增加，inception中1*1、3*3、5*5卷积核的个数增加，可以理解为随着卷积层数的增加，感受野增大，需要更
的卷积核来提取抽象特征。

在V2(增加了batch normalization)和后续版本中继续做了很多优化。可以参考[这里](http://www.mamicode.com/info-detail-1677999.html).


