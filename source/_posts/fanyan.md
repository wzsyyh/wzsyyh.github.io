---
title: 「学习笔记」 二项式反演
date: 2021-10-28 21:30:16
tag: 学习笔记
category: 学习笔记
---

由于大家还没停课所以我很幸运的获得了每一道题的首A。

![](/image/20211028.png)

## 基本形式

$g(k)$ 表示恰好有 $k$ 个满足条件 $S$。

### 形式一：“至少形式”

$f(k)$ 表示至少有 $k$ 个满足条件 $S$。

说是至少其实是因为很多人这么称呼（周神讲课的时候也这么说）。实际上不应当把 $f_k$ 理解为“至少 $k$ 个满足条件 $S$ ”，**而应该理解为“钦定 $k$ 个满足条件 $S$ ，剩下的放任自流”。**

$$f(k) = \sum_{i=k}^{n}{ \binom{i}{k} {g(i)} } \iff g(k) = \sum_{i=k}^{n} (-1)^{i-k} \binom{i}{k} {f(i)} $$

### 形式二：“至多形式”

$f(k)$ 表示至多有 $k$ 个满足条件 $S$。

同样的这并不应当理解成“至多”。

$$f(k) = \sum_{i=m}^{k}{ \binom{k}{i} {g(i)} } \iff g(k) = \sum_{i=m}^{k} (-1)^{n-i} \binom{k}{i} {f(i)} $$

> “至少”形比“至多”形在算法竞赛中更为常用。

上面两个形式证明只需代入。

## 例题

感觉周神给的题目顺序是有在分几种题型的，自己也稍微给题目分了下类。

> 类型1：纯套式子题

### [[BZOJ2839]集合计数](https://hydro.ac/d/bzoj/p/2839)

*AC on 2021.10.28 [CODE](/post/code/#BZOJ2839)*

$$\binom{n}{k} (2^{2^{n-k}}-1) = f(k) = \sum_{i=k}^{n} \binom{i}{k}{g(i)}$$

然后反演就好了。适合作为新手第一题。

### [King's Colors](https://codeforces.com/gym/101933/problem/K)

*AC on 2021.10.28 [CODE](/post/code/#gym101933K)*

题意：$n$ 个点的树填 $k$ 种不同的颜色，求没有相邻两点颜色相同的方案数。

$$k \cdot (k-1)^{n-1} = f(k) = \sum_{i=1}^{k} \binom{k}{i} g(i)$$

### [BZOJ4710 分特产](https://hydro.ac/d/bzoj/p/4710)

*AC on 2021.10.28 [CODE](/post/code/#BZOJ4710)*

$$\binom{n}{k} \prod_{i=1}^{m} \binom{a[i]+n-k-1}{n-k-1} = f(k) = \sum_{i=k}{n} \binom{i}{k} g(i)$$

> 类型2：求反面再套式子题

### [BZOJ4487 染色问题](https://hydro.ac/d/bzoj/p/4487)

*AC on 2021.10.28 [CODE](/post/code/#BZOJ4487)*

题意：$n \times m$ 的矩形，填 $c$ 种不同的颜色，求每行每列都有颜色的方案数。

$f(i,j,k)$ 表示钦定 $i$ 行 $j$ 列一个都没染且钦定 $k$ 种颜色未使用。（即**至少形式**）

$g(i,j,k)$ 表示恰好 $i$ 行 $j$ 列一个都没染且恰好 $k$ 种颜色未使用。

$$f(x,y,z) = \binom{n}{x} \binom{m}{y} \binom{c}{z} (c-z+1)^{(n-x)(m-y)}$$

$$f(x,y,z) = \sum_{i=x}^{n} \sum_{j=y}^{m} \sum_{k=z}^{c} \binom{i}{x} \binom{j}{y} \binom{k}{z} g(i,j,k)$$

一个优化复杂度的小技巧，$O(nm)$ 处理出 $(c-z+1)$ 的 $1$ 到 $nm$ 次方。

### [CF1228E Another Filling the Grid](https://codeforces.com/problemset/problem/1228/E)

*AC on 2021.10.28 [CODE](/post/code/#CF1228E)*

题意：$n \times n$ 的方格纸，$k$ 种数字，求每行、每列最小值均为 $1$ 的方案数。

$f(i,j)$ 表示钦定有 $i$ 行、$j$ 列不满足要求的方案数。（即**至少形式**）

$g(i,j)$ 表示恰好有 $i$ 行、$j$ 列不满足要求的方案数。

$$f(x,y) = \binom{n}{x} \binom{n}{y} (k-1)^{n^2 - (n-x)(n-y)} k^{(n-x)(n-y)}$$

$$f(x,y) = \sum_{i=x}^{n} \sum_{j=y}^{n} \binom{i}{x} \binom{j}{y} g(i,j)$$

> 类型3：需要dp或其他方式先求出 $f(n)$ 的综合题

### [CF997C Sky Full of Stars](https://codeforces.com/problemset/problem/997/C)

*AC on 2021.10.28 [CODE](/post/code/#CF997C)*

题意：$n \times n$ 的网格，用红绿蓝三种颜色染，求至少一行或一列是同一种颜色的方案数。

同样是先求反面（即 $0$ 行 $0$ 列）。不过感觉这题是这几道题目里相当难的一道了。

$f(x,y)$ 表示钦定有 $i$ 行 $j$ 列是同种颜色的方案数。

$g(x,y)$ 表示恰好有 $i$ 行 $j$ 列是同种颜色的方案数。

$$f(x,y) = \sum_{i=x}^{n} \sum_{j=y}^{n} \binom{i}{x} \binom{j}{y} g(i,j)$$

我们要求的是一个 $g(0,0)$，接下来需要算出每个 $f(i,j)$。这个大分类讨论就是难点了。

$$
\begin{aligned}
    f(i,j) &= \binom{n}{i} \binom{n}{j} 3 \cdot 3^{(n-i)(n-j)} &(i,j \neq 0) \\\\
    f(i,0) &= \binom{n}{i} 3^i \cdot 3^{n(n-i)} &(i \neq 0, j = 0) \\\\
    f(0,0) &= 3^{n^2} &(i,j = 0) \\\\
\end{aligned}
$$

于是有：

$$g(0,0) = \sum_{i=0}^{n} \sum_{j=0}^{n} (-1)^{i+j} f(i,j) $$

求和！

两个参数都不为 $0$ 的部分：

$$
\begin{aligned}
    &= \sum_{i=1}^{n} \sum_{j=1}^{n} (-1)^{i+j} \binom{n}{i} \binom{n}{j} 3 \cdot 3^{(n-i)(n-j)} \\\\
    &= 3^{n^2 + 1} \sum_{i=1}^{n} \sum_{j=1}^{n} (-1)^{i+j} \binom{n}{i} \binom{n}{j} 3^{-in-jn+ij} \\\\
    &= 3^{n^2 + 1} \sum_{i=1}^{n} \binom{n}{i} (-1)^i 3^{-in} \sum_{j=1}^{n} \binom{n}{j} (-1)^j 3^{-jn} \cdot 3^{ij} \\\\
\end{aligned}
$$

接下来要消掉 $\sum_{j=1}^{n} \binom{n}{j} (-1)^j 3^{-jn} \cdot 3^{ij}$ 这个烦人的东西：

$$
\begin{aligned}
    \sum_{j=1}^{n} \binom{n}{j} (-1)^j 3^{-jn} \cdot 3^{ij} &= \sum_{j=1}^{n} \binom{n}{j} (-1)^j 3^{j(i-n)} \\\\
    &= \sum_{j=1}^{n} \binom{n}{j} 1^{n-j} (-3^{i-n})^j \\\\
    &= (1-3^{i-n})^n - 1 \\\\
\end{aligned}
$$

最后两行二项式定理转化后面要减去 $1$，因为求和下标不到 $0$。

后面两种情况相对来说好讨论一点，~~不写了~~。其实代码关键部分只有1行

```cpp
for(int i=1;i<=n;i++) (ans+=1ll*((i&1)?(mod-1):1)*C(n,i)%mod*qpow(3,1ll*(mod-1-i)*n%(mod-1))%mod*(qpow((1-qpow(3,i-n+mod-1)+mod)%mod,n)-1+mod)%mod)%=mod;
```

### [BZOJ3622 已经没有什么好害怕的了](https://hydro.ac/d/bzoj/p/3622)

*AC on 2021.10.28 [CODE](\post\code\#BZOJ3622)*

题意：给糖果和药片各 $n$ 个，每个都有一个权值，一一对应搭配。问满足“糖果比药片权值大的”比“药片比糖果权值大的”多恰好 $k$ 个的方案数。

$$dp_{i,j} = dp_{i-1,j} + (L_i - j + 1) \times dp{i-1,j-1}$$

$$f(i) = dp_{n,i} \times (n-i)!$$

$$f(k) = \sum_{i=k}^{n} \binom{i}{k} g(i)$$

反演后 $g(k)$ 就是答案啦。比上面那题简单点。

### [CF285E Positions in Permutations](https://codeforces.com/problemset/problem/285/E)

*AC on 2021.10.28 [CODE](/post/code/#CF285E)*

题意：称一个 $1$ 到 $n$ 的排列的完美数为满足 $|P_i - i = 1|$ 的个数。求有多少个长度为 $n$ 的完美数恰好为 $m$ 的排列。

懒得打dp式了。但确实是一道好题。