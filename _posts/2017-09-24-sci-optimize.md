---
layout: post
title:  Scipy.optimize模块
categories: 机器学习 
tags:  优化算法 
mathjax: true
---

* content
{:toc}

Scipy中的optimieze模块中封装了很多优化算法和求根单元。





## 局部最优化

### 单变量目标函数

* optimize.minimize_scalar-brent  &nbsp;&nbsp;&nbsp;抛物线法一维搜索
* optimize.minimize_scalar-bounded
* optimize.minimize_scalar-golden &nbsp; 黄金分割法

### 通用多变量目标函数

* fmin - Nelder-Mead Simplex algorithm  &nbsp;也叫单纯型，但与下文的单纯型不同，无约束，且不需要知道梯度
* fmin_powell - Powell's (modified) level set method, powell是一个国外大牛
* fmin_cg - Non-linear (Polak-Ribiere) conjugate gradient algorithm   &nbsp; 牛顿共轭梯度法
* fmin_bfgs - Quasi-Newton method (Broydon-Fletcher-Goldfarb-Shanno)  
* fmin_ncg - Line-search Newton Conjugate Gradient   &nbsp; 适用于一般函数的共轭梯度法，如FR

### 受约束的多变量目标函数

bound型约束只是简单的对变量取值范围做约束，constraint型约束：非线性约束

* fmin_l_bfgs_b - Zhu, Byrd, and Nocedal's constrained optimizer; &nbsp; bound型
* fmin_tnc - Truncated Newton code  &nbsp; 截断牛顿法  bound型
* fmin_cobyla - Constrained optimization by linear approximation，constraint型
* fmin_slsqp - Minimization using sequential least-squares programming： constraint型
* differential_evolution - stochastic minimization using differential evolution

## 方程最小化

* leastsq - Minimize the sum of squares of M equations in N unknowns
* least_squares - Feature-rich least-squares minimization.
* nnls - Linear least-squares problem with non-negativity constraint
* lsq_linear - Linear least-squares problem with bound constraints

## 全局优化

启发式算法

* basinhopping - Basinhopping stochastic optimizer 
* brute - Brute force searching optimizer
* differential_evolution - stochastic minimization using differential evolution

## 曲线拟合

* curve_fit -- Fit curve to a set of points

## 线性规划

### 单纯型算法

* linprog -- Linear programming using the simplex algorithm
* linprog_verbose_callback -- Sample callback function for linprog

### Assignment problems

* linear_sum_assignment -- Solves the linear-sum assignment problem

## 公用单元

* approx_fprime - Approximate the gradient of a scalar function，该函数在optmize.py下，在optmize.py中定义了_approx_fprime_helper函数，可以数值化求梯度，其实就是利用导数的定义公式。
* bracket - Bracket a minimum, given two starting points，进退法寻找下单峰区间
* check_grad - Check the supplied derivative using finite differences，计算精确计算梯度和近似计算梯度的差
* line_search - Return a step that satisfies the strong Wolfe conditions,不精确一维搜索
* show_options - Show specific options optimization solvers
* LbfgsInvHessProduct - Linear operator for L-BFGS approximate inverse Hessian

## 补充

* 有一个匈牙利算法，解决带权重的二分图匹配
