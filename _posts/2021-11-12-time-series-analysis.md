---
layout: post
title: "Time Series Data Analysis"
category: Quant
tags:
  - Quant
  - Regression
  - TimeSeries
---

> About R language and time series analysis: garch, aram.



### 1. R language

参考官网的 [cheatsheet](https://www.rstudio.com/resources/cheatsheets/). Packages: [some useful packages info](https://www.math.pku.edu.cn/teachers/lidf/course/fts/ftsnotes/html/_ftsnotes/rsoft.html#rsoft-ts-misc) of TS analysis.

#### 1.1 questions

###### 1. Why use `d[["rate"]]`?

In fact, use `d["rate"]`also  working well.

```R
d <- read.table(
  "./ftsdata/m-unrate.txt", header=TRUE,
  colClasses=rep("numeric", 4))
unrate <- ts(d[["rate"]], start=c(1948,1), frequency=12)
plot(unrate)
```

###### 2. pipe function `%>%` 

`x %>% f` means `f(x)`, why I use it? To <u>save memory</u>.

###### 3. `getSymbols` useless

Found [solution 1](https://www.codenong.com/44015838/). But when I use it, it will open my browser to download the data, which means thta one more step, reading the data from file is needed.  And VPN should be open. It works anyway.

> Copied from [https://www.codenong.com/44015838/](https://www.codenong.com/44015838/)

###### 4. `coredata(x)`

> Generic functions for extracting the core data contained in a (more complex) object and replacing it.

大概是将一些复杂的对象建立的数据（如 `xts` ）转化为 `R` 的普通数据类型。

###### 5. `package::function`

不用 `library(function)`，避免不同包的重名函数和`library`的其他附带作用。

### 2. Financial data

#### 2.1 return

Correlation between <u>log return</u>($r_t$) and <u>simple return</u>($R_t$).
$$
r_t = \ln \frac{P_t}{P_{t-1}} = \ln(\frac{P_t - P_{t-1}}{P_t} + 1) = \ln (R_t + 1)
$$
An example:

```R
# draw the log returns
chartSeries(
  logret.AAPL, # xts style data
  subset = "2020/2020", # to get subset from xts style date
  theme = chartTheme("white"),
  name = "2020 APPLE Log Returns",
  major.ticks = "months", minor.ticks = FALSE
)
# histgram of log returns
x <- coredata(logret.AAPL[-1])
hist(x, main = "Apple Log Returns", xlab = "log return(%)", ylab = "density")
# normal qqplot of log returns
qqnorm(x, main="Apple Log Returns")
qqline(x, col="blue")
```

Output:

![](https://i.bmp.ovh/imgs/2021/11/099c27957a730db9.png)

![](https://i.bmp.ovh/imgs/2021/11/5d3730c8e08179cb.png)

![](https://i.bmp.ovh/imgs/2021/11/379954313755cb36.png)

#### 2.2 statistics distribution

Just look at [here](https://www.math.pku.edu.cn/teachers/lidf/course/fts/ftsnotes/html/_ftsnotes/fts-intro.html#intro-returnstat). Some keys below.

计算基本统计量：`basicStats()`in library  `fBasics`.

```R
fBasics::basicStats(x)
```

continuation...

### 3. Linear time series model



















### 18. Garch Model

#### 18.1 Garch model

对数收益率序列 $r_t$，新息序列$a_t = r_t - \mu_t = r_t - E(r_t\|F_{t-1})$，称 $a_t$ 服从 $GARCH(m,s)$模型若满足：


$$
\left\{
\begin{aligned}
& a_t = \sigma_t  \epsilon_t; \ \ \sigma_t^2 = \alpha_0 + \sum_{i=1}^m \alpha_i a_{t-1}^2 
+ \sum_{j=1}^s \beta_j \sigma_{t-j}^2 \\
& \sigma_t \sim \text{i.i.d WN} (0,1^2) \\
& \alpha_0 > 0; \alpha_i \geq 0;  \beta_j \geq 0  \\
& 0 < \sum_{i=1}^m \alpha_i + \sum_{j=1}^s \beta_j < 1
\end{aligned}
\right.
$$



最后一个条件用来满足 $E(a_t)$ 有限且不变。但是 $E(\sigma_t^2 \boldsymbol | F_{t-1})$ 可以变化。





