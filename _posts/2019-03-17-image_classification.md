---
layout: post
title:  图像模型
categories: 经典CNN
tags:  CV
mathjax: true
---

* content
{:toc}

图像的模型发展简介，Xception、Resnet、Densenet、Mobilenet





## depthwise separable convolution

常规卷积，一个卷积核要在所有通道上卷积，depthwise separable convolution将通道间解耦，现在每个通道上都卷积，再使用1*1的卷积聚合，优点是压缩了参数数量。

<div align="center"><img src="/photoes/2019/depth_conv.png" /></div>

<div align="center"><img src="/photoes/2019/depth_conv1.png" /></div>

## Resnet

随着模型深度的增加，模型在训练集上准确率下降了，无法解释为过拟合，说明层数加深模型却退化了，原作者提出了shutcut,$y=H(x)+x$。以残差块为基本组成单位。
当channels不同时，先通过卷积变换在相加。

<div align="center"><img src="/photoes/2019/resnet.png" /></div>

## Densenet

在Resnet基础上，将当前层输出与后面所有层的输出连接。Densenet的密连接是指dense block中密连接，Densenet是有多个denseblock组成。

<div align="center"><img src="/photoes/2019/densenet.png" /></div>

<div align="center"><img src="/photoes/2019/densenet.png" /></div>

bottleneck指其中的1*1卷积，减少channels个数，channels个数为4k；transition layer也是1*1卷积，通过参数$\theta$控制channels数量，
为$\theta*m$，m为上一层的输出channels数量。

## Xception

Xception同时借鉴了depthwise separable convolution和resnet的思想，减少参数数量，加速收敛

pointwise convolution:1*1卷积

<div align="center"><img src="/photoes/2019/xception.png" /></div>

## mobilenet

为移动和嵌入式设备设计，轻量型模型，使用了depthwise separable convolution。涉及到模型的压缩方法，在模型复杂度和准确率间作平衡。

## SEnet

## Siamse Net
