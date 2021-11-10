---
layout: post
title: "Fixed and Random Effect Model"
category: Quant
tags:
  - Quant
  - Regression
  - Panel Data
---



> About "Fixed Effect Model" and "Random Effect Model" in panel data.

Reference: [面板数据回归分析，上财经济学院](https://max.book118.com/html/2018/0705/5034012214001301.shtm)



$$
\begin{aligned}
& y_ {it} = \alpha _ i + \boldsymbol X_{it} \boldsymbol \beta + u_{it} \\
& i = 1, 2, \cdots, N. \text{and } t = 1, 2, \cdots, T
\end{aligned}
$$


$\boldsymbol X_{it}$ ——1 by k; 	$\boldsymbol \beta$——k by 1, 其中 k 为解释变量的个数。

其余的假设：$u_{it}$ 为随机扰动项，

其中 $\alpha_i$ 为个体异质性。

个体异质性分为两种情况：

1. 与解释变量相关（即为内生性问题），固定效应模型；
2. 与解释变量无关，称之为随机效应模型。

##### 1. FEM

消除方法有两种，分别为 FE 和 FD

1. FE：时间方向上取平均，再样本减去平均，消除$\alpha _ i$
2. FD (First Difference)：相邻时间点样本作差，也可消除。

##### 2. REM

将个体异质性归入随机误差项，


$$
v_{it} = u_{it} + \alpha_i
$$


但是此时不能用 OLS 估计，因为 $v_{it}$ 不满足不相关假设，即协方差矩阵不是 $\sigma^2 I_{nT}$，即要用 GLS 得到最优估计。（这个就是金融计量课上讲 GLS 为什么要用这个例子的地方了）。

> 讲义里面构造 $\theta$ 的时候需要知道 $\sigma_u^2$ 和 $\sigma _ \alpha ^ 2$，实际中这二者并不知道，需要一些方法进行估计：Swamy-Aora, Wallace- Hussaini,  Wansbee Kapteyn方法，常用第一种方法。

#####  如何选择模型？

详细请见 Hausman 检验。









