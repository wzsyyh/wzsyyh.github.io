---
title: 「学习笔记」决策单调性dp/斜率优化dp
date: 2021-06-30 11:39:17
tag: 动态规划
category: 学习笔记
---
听周神讲完，对此有些新的理解吧

### 证明决策单调性，不会四边形不等式也没关系

先以经典题[P2900 [USACO08MAR]Land Acquisition G/土地购买](https://www.luogu.com.cn/problem/P2900)为例。

$$f[i]=\min\{f[j]+y[j+1] \times x[i]\}$$

用 $g[i]$ 表示转移到 $f[i]$ 最优的决策点，证明 $g[i]<=g[i+1]$ ：

根据 $g[i]$ 的定义，相当于已知了（下面 $j$ 为任意决策点）

$$f[g[i]]+y[g[i]+1] \times x[i]≤[j]+y[j+1] \times x[i]$$

那等价于证明：

$$f[g[i]]+y[g[i]+1] \times x[i+1]≤f[j]+y[j+1]\times x[i+1]\ \ \ \ (j≤g[i])$$

利用已知：

$f[g[i]]+y[g[i]+1] \times x[i+1]+y[g[i]+1] \times (x[i]-x[i+1])≤f[j]+y[j+1] \times x[i+1]+y[j+1] \times (x[i]-x[i+1])$

$∵j≤g[i]\ ∴y[g[i]+1]≤y[j+1]$

$∵x[i]<x[i+1]\ ∴x[i]-x[i+1]<0$

$∴y[g[i]+1] \times (x[i]-x[i+1])≥y[j+1] \times (x[i]-x[i+1])$

$∴f[g[i]]+y[g[i]+1] \times x[i]<=f[j]+y[j+1] \times x[i]$ 

### 2D1D和1D1D

不过我好像也不是很清楚

但1D1D似乎是可以用斜率优化的，2D1D只能二分或者分治？