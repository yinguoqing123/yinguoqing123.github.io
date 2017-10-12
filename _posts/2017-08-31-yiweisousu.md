---
layout: post
title:  "一维搜索"
categories: 凸优化 
tags:  一维搜索  goldstein准则 wolf准则 
mathjax: true
---

* content
{:toc}

本文主要介绍凸优化中，精确一维搜素和不精确一维搜素方法和准则，求解$min f(\mathrm x_k+\alpha \mathrm p_k)$,$\alpha$为变量。





## 精确一维搜索

### 黄金分割法

要求：$ f(x)$是在区间$[a,b]$上的下单峰区间，在此区间上可以寻找$ f(x)$的最小值

区间每次缩减0.618

### 抛物线法(二次插值法)

用多项式逼近函数

### 二分法

要求：$f(x)$的导数有解析表达式

区间每次缩减一半

## 不精确一维搜素

### Goldstein准则

1. 步长不能太小，否则相当于原地打转。
2. 函数值应当充分地下降。

$$
f(\mathrm x_k + \alpha_k \mathrm p_k) \le f(\mathrm x_k) + \alpha_k \rho g_k^T p_k \tag{1}
$$

$$
f(\mathrm x_k + \alpha_k \mathrm p_k) \ge f(\mathrm x_k) + \alpha_k (1-\rho) g_k^T p_k \tag{2}
$$

其中$0\lt\rho\lt 1/2$,否则会影响牛顿法或拟牛顿法的超线性收敛。

![](/photoes/201709_10/yiweisousuo.png)

缺点：如上图所示，$\alpha$取值区间在$[b,c]$中，很容易漏掉真正的极小点。

### Wolf准则

改进上述缺点,使得取值区间包含真正的极小值点,将上式中的条件2改为下式,且$\sigma\subset\(\rho,1)$：

$$
\nabla f(\mathrm x_k + \alpha_k \mathrm p_k)^T \mathrm p_k \ge \sigma \mathrm g_k^T \mathrm p_k
$$

加强的Wolf准则:

$$
\lvert \nabla f(\mathrm x_k + \alpha_k \mathrm p_k)^T \mathrm p_k \rvert \le \lvert \sigma \mathrm g_k^T \mathrm p_k \rvert
$$

解释为可接受点处的切线斜率大于等于才初始斜率的$\alpha$倍。

函数$min f_\alpha(\mathrm x_k+\alpha \mathrm p_k)$对$\alpha\$求导结果：$\frac{\partial f}{\partial \alpha}=\frac{\partial f}{\partial (\mathrm x_k + \alpha \mathrm p_k)} \frac{\partial (\mathrm x_k + \alpha \mathrm p_k)}{\mathrm x_k}$,即$\nabla f(\mathrm x_k + \alpha_k \mathrm p_k)^T \mathrm p_k$

#### 示例

用不精确一维搜索求Rosenbrock函数：$f(x)=100(x_2-x_1^2)^2+(1-x_1)^2$在点$\mathrm x_k=(0,0)^T$沿方向$\mathrm p_k=(1,0)^T$的近似步长$\alpha_k$。

python3代码：

```python
import numpy as np
def rosenbrock(x):
    return 100*(x[1]-x[0]**2)**2 + (1 - x[0])**2

def jacobian(x):
    return np.array([-400*x[0]*(x[1]-x[0]**2)-2*(1-x[0]),200*(x[1]-x[0]**2)])

def goldsteinsearch(f, df, p, x0, rho, alpha=1, a=0, b=float("inf"), t=2):
    """

    :param f:  输入函数
    :param df:  梯度
    :param p: 搜索方向
    :param x0: 初始点
    :param a, b: alpha取值区间
    :param alpha: alpha初始值
    :param rho: 参数 (0, 1/2)
    :param t:  参数
    :return:  适当的步长alpha
    """
    flag=0

    fk=f(x0)
    gk=df(x0)

    phi0=fk
    dphi0=np.dot(gk,p)

    while(flag==0):
        newfk=f(x0+alpha*p)
        phi=newfk
        if(phi-phi0<=rho*alpha*dphi0):
            if(phi-phi0>=(1-rho)*alpha*dphi0):
                flag=1
            # alpha 不够大
            else:
                a=alpha
                b=b
                if(b != float("inf") ):
                    alpha=(a+b)/2
                else:
                    alpha=t*alpha
        # alpha 不够小
        else:
            a=a
            b=alpha
            alpha=(a+b)/2
    return alpha


def wolf(f, df, p, x0, rho, sigma, alpha=1, a=0, b=float("inf"), t=2):
    '''

    :param f: 输入函数
    :param df: 函数梯度
    :param p: 搜索方向,
    :param x0: 初始点
    :param rho: 参数
    :param mu: 参数
    :param alpha:初始步长
    :param a, b: alpha取值区间
    :return: 满足条件的步长
    '''
    flag = 0
    f_0 = f(x0)
    g_0 = df(x0)

    while(flag == 0):
        x_k = x0 + alpha * p
        f_k = f(x_k)
        g_k = df(x_k)
        if (f_k <= f_0 + alpha*rho*np.dot(g_0, p)):
            if (np.dot(g_k, p) >= sigma*np.dot(g_0, p)):
                flag = 1
            # alpha 不够大
            else:
                a = alpha
                if b == float("inf"):
                    alpha = t*alpha
                else:
                    alpha = min(2*alpha, (alpha+b)/2.0)
        # alpha 不够小
        else:
            b = alpha
            alpha = (a + alpha) / 2.0;

    return alpha

p = np.array([1, 0])
x0 = np.array([0, 0])
f = wolf(rosenbrock, jacobian, p, x0, 0.1,0.5)
print("最终搜素的alpha值：", f)  # 最终搜素的alpha值：0.125
g = goldsteinsearch(rosenbrock, jacobian, p, x0, 0.1 )
print("最终搜索的alpha值：", g)

```








