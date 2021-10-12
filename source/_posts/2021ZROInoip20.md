---
title: 「游记」2021ZROI联赛
date: 2021-10-12 18:20:28
tag: 游记
category: 游记
---

感觉需要记录下每天的收获吧。

### 10.11

一些杂题。~~记得补~~。

### 10.12

第一场模拟赛，考得很不理想。

#### T1

事实上赛时已经把条件转换的很彻底了：

$$y=(a+b) \% p$$

$$c=xa-x'y$$

$$x'<x$$

于是我枚举了 $x$ 并在内层继续枚举 $x'(0≤x'<x)$。

然而，其实我只需要枚举 $x$ 并且判断

$$\frac{xa-c}{y} \% p<x$$

这个式子是否成立即可 AC 。。。

#### T2

其实感觉这题 xtq 给的题解做法还是很玄学，只要数据是手造的就可以卡掉了。

不过这个题正解也给了一定启发吧，**题目的数据范围都是出题人精心准备的**。

于是此题，比 $25$ 大的与比它小的分开处理，巧妙利用了 $2^{25}$ 的大小。

#### T3

赛时没怎么花时间好好想，其实好好分类讨论一下还是可做的。

#### T4

**题目的数据范围都是出题人精心准备的**。这题的数据范围非常的骗人。。。$n≤2 \times 10^5$ 的范围，正解却是 $O(n)$。这说明不能全看数据范围判断正解复杂度。

赛时没有写出一个像样的简明的递推式，最后只写了区间dp拿了20pts。这种能力不知道咋锻炼。