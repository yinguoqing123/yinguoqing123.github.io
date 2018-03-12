---
layout: post
title:  矩阵相乘的几种写法
categories: 数学
tags:  矩阵乘法
mathjax: true
---

* content
{:toc}

矩阵可以看做行向量的组合或列向量的组合。





## 矩阵乘法

假设有两个矩阵$A$和$B$，且$AB=C$。

$$
A=\left[
   \begin{matrix}
   1 & 2 & 3 \\
   4 & 5 & 6 
  \end{matrix} \right]  \quad
  
B =\left[
   \begin{matrix}
   1 & 2  \\
   0 & 0 \\
   1 & 2 
  \end{matrix} \right]  \quad

C =\left[
   \begin{matrix}
   4 & 8  \\
   10 & 20 
  \end{matrix} \right]   
$$

### 列向量线性组合

$$
1 \cdot \left( 
	\begin{matrix}
	1 \\ 4
	\end{matrix} 
	\right)  + 
0 \cdot
	\left( 
	\begin{matrix}
	2 \\ 5
	\end{matrix} 
	\right)  + 
1 \cdot
	\left( 
	\begin{matrix}
	3 \\ 6
	\end{matrix} 
	\right) 
=
\left( 
\begin{matrix}
	4 \\ 10
\end{matrix} 
\right)	
$$

### 行向量线性组合

$$
1 \cdot (1,2) + 2 \cdot (0, 0) + 3 \cdot (1,2) = (4, 8)
$$

### 整体乘法分解

$$
\left( 
	\begin{matrix}
	1 \\ 4
	\end{matrix} 
\right) (1,2) + 
\left( 
	\begin{matrix}
	2 \\ 5
	\end{matrix} 
	\right) (0, 0) +
\left( 
	\begin{matrix}
	3 \\ 6
	\end{matrix} 
	\right) (1, 2) = 
\left(
   \begin{matrix}
   4 & 8  \\
   10 & 20 
  \end{matrix} \right)
$$