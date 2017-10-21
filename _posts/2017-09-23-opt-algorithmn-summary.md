---
layout: post
title:  机器学习常见算法汇总
categories: 机器学习
tags:  优化算法
mathjax: true
---

* content
{:toc}

对机器学习中常用的优化算法的汇总，其实有一些我自己也不是很了解，这些算法在scipy库和scikit-learn中都有涉及与实现代码。





## 算法汇总

* 梯度下降类：[参考](http://blog.csdn.net/sun_shengyun/article/details/53811882),包括SGD,SAG等，计算量与收敛速度的平衡
* 牛顿法、共轭类、拟牛顿法：BFGS、newton-cg等，牛顿法需要目标函数二阶可导
* L-BFGS算法：对BFGS算法：对BFGS算法的改进，极大的节省了存储空间,[参考](http://blog.csdn.net/itplus/article/details/21897715)
* LSQR(最小平方QR分解，在LDA中用到，[参考](http://web.stanford.edu/group/SOL/software/lsqr/))[豆丁](http://www.doc88.com/p-3307764572398.html)
* LARS(最小角度回归)，坐标下降，不需要知道梯度，求解Lasso回归，缺点是对噪声非常敏感。[参考1](http://www.cnblogs.com/pinard/p/6018889.html)[参考2](http://statweb.stanford.edu/~tibs/lasso/simple.html)
* [OMP](http://blog.csdn.net/jbb0523/article/details/45130793),正交匹配追踪，重点在于观测矩阵和变换矩阵如何寻找
* SMO(Sequential Minimal Optimization),在SVM中用到[参考文章](http://blog.csdn.net/luoshixian099/article/details/51227754)
* [EM算法](http://www.cnblogs.com/Gabby/p/5344658.html),吉布斯采样，概率图中关键
* 遗传算法、粒子群、蚁群优化

