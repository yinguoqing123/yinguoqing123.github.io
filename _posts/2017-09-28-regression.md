---
layout: post
title:  线性方程组的解和矩阵分解基础
categories: 数学基础
tags:  最小二乘解  矩阵分解
mathjax: true
---

* content
{:toc}

方程组解、最小二乘解、极小范数最小二乘解的结论性资料，有关证明可另搜索。另简单介绍矩阵的多种分解。






## 最小二乘

为什么在回归分析中都使用最小二乘，这是假设噪声是高斯白噪声，按照最大化贝叶斯后验概率求解而得，即使两个向量的距离最小，若对噪声的假设
不同，那么可以不用最小二乘。

## 方程组的解

方程组：$A \mathrm x = \mathrm b $

* 方程组有唯一解：$\mathrm = A^{-1} \mathrm b$
* 方程组有无穷多组解:可以求无穷多解中的最小范数解，即 $\Vert x \Vert_2 = \min \limits_{A \mathrm x = \mathrm b} \Vert \mathrm x \Vert_2$
* 方程组无解：可以求解最小二乘解,即$\Vert A \mathrm x - \mathrm b \Vert_2 = \min \limits_{\mathrm x \in R^n}
\Vert A \mathrm x - \mathrm b \Vert_2$,一般来说最小二乘解是不唯一的，所以可以更进一步求极小范数最小二乘解，即在最小二乘解组成的集合
中求$\mathrm x$, 满足$\Vert \mathrm x \Vert_2 = \min \Vert \mathrm x \Vert_2$

## 矩阵广义逆

对任意复矩阵$A \in C^{m \times n}$, 若存在$G \in C{n \times m}$,满足四个Penrose方程中一个或几个，则称$G$为$A$的一个广义逆矩阵：

1. $AGA = A$
2. $GAG = G$
3. $(AG)^H = AG$
4. $(GA)^H = GA$

若全部满足，则称$G$为$A$的Moore-Penrose逆，记作$G = A^+$；

显然，若$A可逆$，$A^{-1}$满足上面四个方程。

### 加号逆的计算

1. 若$A$为满秩矩阵，则$A^+ = A^{-1}$
2. 若$A$为行满秩矩阵，则$A^+ = A^H(AA^H)^{-1}$
3. 若$A$为列满秩矩阵，则$A^+ = (A^HA)^{-1}A^H$
4. 若$A$为降秩矩阵，先求满秩分解，$A = FG$,(满秩分解不唯一)，其中$F$为列满秩,$G$为行满秩，则$A^+ = G^+F^+=G^H(GG^H)^{-1}(F^HF)^{-1}F^H$

## 方程组解的形式

若$rank(A\|\mathrm b) = rank(A)$,则称方程组为相容方程组，方程组有解；否则称为矛盾方程组，方程组无解。

### 相容方程组

定理：

* 齐次方程组$A \mathrm x = 0$的通解为$\mathrm x = (I^{-1}-A^+ A)Y, Y \in R^n$.
* 非齐次方程组$A\mathrm x = \mathrm b$是相容方程组的充要条件是$AA^+b=A\mathrm b$
* 设非齐次方程组$A\mathrm x = \mathrm b$是相容的，则:
	* 其通解是:$\mathrm x = A^+ \mathrm b + (I-A^+ A)Y), Y \in R^n$;
	* 其唯一的极小范数解是：$\mathrm x = A^+ \mathrm b$
	
### 矛盾方程组

定理:

1. $\mathrm x$是矛盾方程组$A \mathrm x = \mathrm b$的最小二乘解的充要条件是$\mathrm x$ 是方程组$A^H A \mathrm x = A^H \mathrm b $的解。
2. 非齐次方程组$A \mathrm x = \mathrm b$是不相容的，则
	* 其最小二乘解的通解是：$\mathrm x = A^+ \mathrm b + (I - A^+A)Y, Y \in R^n$
	* 其唯一的极小范数最小二乘解是：$\mathrm x = A^+\mathrm b$
	
## 矩阵分解

1. LU分解：分解成上三角矩阵和下三角矩阵相乘。<br/>
推论：$A$可分解为$A = LU$,当且仅当$A$的前$n-1$个顺序主子式都不为0；</br>
定理：$A$非奇异，则存在置换矩阵P使得$PA$的n个顺序主子式都非0.
2. 满秩分解:$A = FG$,$F$为列满秩,$G$为行满秩，任何非零矩阵都可以进行满秩分解，满秩分解不唯一。
3. QR分解：$A$为方阵，分解成酉矩阵和上三角矩阵的乘积；矩阵$A$非奇异，则可QR分解。
4. 奇异值分解：任意矩阵可进行奇异值分解。

## 补充

机器学习中的正则化项：

为了获得模型的一些结构，会加入正则化项，最常用的是L1和L2范数。正则化项也可以防止过拟合。

L2范数可以限制$\mathrm w$的每个分量都接近与0

L1范数可以稀疏化$\mathrm w$，当样本数远小于特征数时，应当使用L1范数，因为实际上特征之间存在线性关系，应当是$\mathrm w$尽量稀疏化

[参考](http://blog.csdn.net/qiao1245/article/details/53020882)

