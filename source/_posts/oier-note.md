---
title: OI日志
date: 2021-01-31 16:23:26
tag: 学习笔记
category: 学习笔记
---
**[view in Push_Y's blog](https://www.wzsyyh.ml/post/OI-note/)**

**[view in 博客园](https://www.cnblogs.com/wzsyyh/p/oier-note.html)**

**[view in 洛谷博客](https://www.luogu.com.cn/blog/wzsyyh/oier-note)**

2021.01.26 来WZHS了有望复出

2021.01.31 发现东西都忘光了，得从基础的基础开始复习了。。。

2021.03.10 发现真正做题之后根本不会记得来这里记录，很能拖更啊。。。

2021.05.10 月赛后涨了30左右，第一次红名 QwQ

2021.05.12 搭建了[新的博客](https://wzsyyh.ml)

2021.06.24 中考阅卷占用的机房回归了，由于在机房，只能在洛谷博客上更了。

2021.07.12 正式拿到了WZHS的录取通知书。

2021.08.21 明天新生报道了，要正式开启高中生涯了。

2021.09.24 ~~晚上20:21野狐5段了~~

2021.10.06 将目标中的 p 改回了 t 。

2021.10.16 第一次尝试咖啡，准备在一周后的csp考场上使用。

2021.10.19 **传6个参数的merge函数会编译错误！！！**

2021.11.03 夜聊讨论概率问题被宿管抓住，次日在班主任眼皮底下罚跑10圈QwQ

## 专题

> 以下专题按 [Push_Y](https://www.luogu.com.cn/user/135485) 复出后接触的时间先后排列

### [基础dp](/)
  
- 2021.01.31 [UVA437 The Tower of Babylon](https://www.luogu.com.cn/problem/UVA437)

### [状压dp](https://oi-wiki.org/dp)

- 2021.02 写了一些比较简单的状压，就不放上来了

- 2021.06.29 [[WZOI]奶牛的食物](https://wzoi.cc/s/1618/2195) 从02.04的50分一直咕到今天闲着没事干才改
    
- 状压难起来还是挺难的QwQ

- 2021.06.29 [[WZOI]简单签到题](https://wzoi.cc/s/1618/2883)

	- 我的代码上题解了！~~其实近似于抄的~~

	- 一个`f[i]`存子树状态为i的有根树方案数，一个`sum[i]`存含状态i的森林方案数

- 2021.06.29 [UVA12235 Help Bubu](https://www.luogu.com.cn/problem/UVA12235) ATue秒掉的黑题，但我觉得挺难的

- 2021.06.29 [Sgu P131铺地板](https://wzoi.cc/s/1618/623) 有时状压用递归的形式来写很方便

- 2021.06.30 [P3204 [HNOI2010]公交线路](https://www.luogu.com.cn/problem/P3204)

	- 题意比较难理解吧。晚上做的这题，那个转移让我心态崩了，浑身无力直接瘫电脑前了。

### [树形dp](https://oi-wiki.org/dp/tree/)

- 2021.01.31 [[POI2014]FAR-FarmCraft](https://www.luogu.com.cn/problem/P3574) 中间遍历子树顺序不能换

- 2021.04.15 [[WZOI]粉兔找妹子](https://wzoi.cc/s/1605/3348) 从2.13的60分（暴力）一直咕到今天才补。今天重写了个换根dp。~~好难改~~
    
### [分治](https://oi-wiki.org//misc/cdq-divide/) 
  
- 2021.02.17 [平面最近点对（加强版）](https://www.luogu.com.cn/problem/P1429) 平面分治，关键在合并
 
- 2021.03.10 [摆放L](https://wzoi.cc/s/1605/550)
	- 好巧妙的构造！
	- 每次把棋盘分割成4份进行分治，使得每份各有一黑格 

- 2021.07.05 [[十一集训A班day1]奖杯](http://www.zhengruioi.com/contest/711/problem/1584)

### [基环树](https://www.luogu.com.cn/blog/user52918/qian-tan-ji-huan-shu)

- 2021.04.19 [P5022 [NOIP2018 提高组] 旅行](https://www.luogu.com.cn/problem/P5022) 拓扑排序找环，$O(n^2)$ 暴力断边dp

### [仙人掌](/)

### [树链剖分](/)

- 2021.07.18 [[POJ3728]The merchant](http://poj.org/problem?id=3728) 树剖写的话要转好几下

### [长链剖分](/)

### [cdq分治](/)

- 2021.05.30 [[NOI2007] 货币兑换](https://www.luogu.com.cn/problem/P4027)

	- [笔记](https://www.wzsyyh.ml/post/huobiduihuan)
    
### [数位dp](https://oi-wiki.org/dp/number/)

- 2021.03.30 [P4127 [AHOI2009]同类分布](https://www.luogu.com.cn/problem/P4127) 枚举模数这里有点难懂
    
- 2021.03.30 [P3413 SAC#1 - 萌数](https://www.luogu.com.cn/problem/P3413) 转移方程里的 $k$ 有点难懂

- 2021.03.30 [准考证](https://wzoi.cc/s/1618/1159) 适合作为板子题之后自己写的第一题

### [数据结构优化dp](/)

- 某月某日 [基站选址](/)
    
- 2021.06.28 [ABC207E](https://atcoder.jp/contests/abc207/tasks/abc207_e)

	- 赛时只想到 $O(n^3)$ ，原来异或也能前缀和，前缀和优化一下就能 $O(n^2)$ 过了

- 2021.07.09 [[十一集训A班day2]计](http://www.zhengruioi.com/problem/1590)

	- 去年十一的时候考的题。当时可能并没有完全理解。

	- 前缀和不一定是 $sum_i=a_1+a_2+...+a_n$ ，像这题就是 $sum_i=sum_{i-2}+a_i$ 。

- 2021.07.12 [[ABC209F] Deforestation](https://atcoder.jp/contests/abc209/tasks/abc209_f) 还是前缀和优化。近阶段其实很多dp优化都是用前缀和优化。

- 2021.07.28 [[CE2003] Minimizing maximizer](http://poj.org/problem?id=1769) 经典线段树维护dp，写法跟线段树维护最长上升子序列很像。

> bitset优化！

- 2021.10.14 [[zr联赛集训day3]史上第三简洁的题面](http://www.zhengruioi.com/problem/2018) 或许是第一次遇到bitset优化dp。能用bitset优化的原则应当是状态全都是bool型。

### [决策单调性/单调队列/斜率优化dp](https://www.cnblogs.com/MashiroSky/p/6009685.html)

- **疑难点**：推柿子；单调队列里 $l$ 与 $r$ 的关系（是 $＜$ 还是$≤$），以后习惯 `l=r=1;q[1]=0;` 并且维护队列部分用 `l<r`。
    
- 2021.4.12 [P3648 [APIO2014]序列分割](https://www.luogu.com.cn/problem/P3648) 看着题解写完了一些斜率优化题之后，这题开始尝试自己推柿子

- 2021.4.14 [CF311B Cats Transport](https://www.luogu.com.cn/problem/CF311B) 
    
	- 题目给的信息过多，难想到先**按“每只猫子所需出发时间”排序再斜率优化**。
        
	- 粗略一看题解区绝逼互抄的，既然大家都想到开一个 $g[]$ 存上一轮状态了为什么 $f[]$ 不用滚动？
        
- 2021.05.30 [[NOI2007] 货币兑换](https://www.luogu.com.cn/problem/P4027)

	- [笔记](https://www.wzsyyh.ml/post/huobiduihuan)
        
	- 2021.06.29 周神今天讲了下决策单调性和斜率优化，准备写篇笔记记下心得

- 2021.06.29 [P4544 [USACO10NOV]Buying Feed G](https://www.luogu.com.cn/problem/P4544) 单调队列

- 2021.06.30 [P2900 [USACO08MAR]Land Acquisition G/土地购买](https://www.luogu.com.cn/problem/P2900) 很好的联系推式子的题了，但预处理折腾了我好久。。。

### [强连通分量](https://oi-wiki.org/graph/scc/) 和 [2-SAT](https://oi-wiki.org/graph/2-sat/)

- 2020.10.04 写了[2-SAT模板题题解](https://www.luogu.com.cn/blog/wzsyyh/solution-p4782)

- 2021.04.21 写了[题解 [POI2001] 和平委员会](https://www.luogu.com.cn/blog/wzsyyh/solution-p5782)

### [左偏树](https://oi-wiki.org/ds/leftist-tree/)

- [学习笔记](https://www.luogu.com.cn/blog/wzsyyh/xxbj-zps)

### [矩阵](https://oi-wiki.org/math/matrix/)

- 2021.04.24 [P2151 [SDOI2009]HH去散步](https://www.luogu.com.cn/problem/P2151) **点边转换**处理不能走重边

- 2021.04.24 [P2886 [USACO07NOV]Cow Relays G](https://www.luogu.com.cn/problem/P2886) 定义新的矩阵乘法规则
    
	- 2021.06.25 听周神讲了才知道，原来min/max(a[i][k]+b[k][j])也可以当做不规则的矩乘，ATue表示其实就是说符合结合律的运算都可以套矩乘。

### [平衡树](https://oi-wiki.org//ds/splay/)

- [Splay学习笔记](https://www.luogu.com.cn/blogAdmin/article/edit/313751)

- 2021.06.24 [维护数列](https://www.luogu.com.cn/problem/P2042) 好板子
    
- 2021.06.25 [[bzoj3678]/[wzoi] wangxz与OJ](https://darkbzoj.tk/problem/3678)

	- 开始看似就是维护数列那题的子问题，结果T飞了。

	- 此题插入区间时不直接插入完，而是插入一个结点并保留区间信息，用到时再下传。

- 2021.06.25 [P3960 [NOIP2017 提高组] 列队](https://www.luogu.com.cn/problem/P3960)

	- [笔记](https://www.wzsyyh.ml/post/duilie/)

- 2021.07.12 [P3215 [HNOI2011]括号修复 / [JSOI2011]括号序列](https://www.luogu.com.cn/problem/P3215) 请来麻大师改了半天，错误居然出现在`k-=sz[ch[x][0]]+1;`老黄油手了。

- 2021.07.12 [P4036 [JSOI2008]火星人](https://www.luogu.com.cn/problem/P4036) 初始化忘记`rt=1`了????

### [整体二分](https://oi-wiki.org//misc/parallel-binsearch/)

- 2021.05.01 AC了板子 [P3834 【模板】可持久化线段树 2（主席树）](https://www.luogu.com.cn/problem/P3834) 和 [P2617 Dynamic Rankings](https://www.luogu.com.cn/problem/P2617)
    
- 2021.05.03 [P3527 [POI2011]MET-Meteors](https://www.luogu.com.cn/problem/P3527)
    
	- 感觉每个询问的id都是它序号本身，所以`ans[q[i].id]=l`写成了`ans[i]=l`，不知道为什么错。

- 2021.05.04 [P3242 [HNOI2015] 接水果](https://www.luogu.com.cn/problem/P3242) 这题主要难在树上路径覆盖条件的转化

- 2021.05.04 [P3332 [ZJOI2013]K大数查询](https://www.luogu.com.cn/problem/P3332)

	- 区间询问区间查询，数据结构选择线段树

	- 之前的板子和例题都是第k小，这题要q1和q2反过来

### [点分治](https://oi-wiki.org/graph/tree-divide/)

- 2021.05.05 [P4178 Tree](https://www.luogu.com.cn/problem/P4178) 经典题

- 2021.05.05 [P3806 【模板】点分治1](https://www.luogu.com.cn/problem/P3806)

- 2021.05.08 [[bzoj3648]寝室管理/[wzoi]点分治2](https://darkbzoj.tk/problem/3648)

	- 吐了，改了一晚上，最终是 ATue 神佬找到了错误QwQ。。。

	- upd:05.09 bzoj上还过不了，可能像 ATue 说的那样环编号得是在环上连续的吧，~~懒得改了~~

- 2021.05.09 [[hdu4812]D Tree/[wzoi]点分治3](http://acm.hdu.edu.cn/showproblem.php?pid=4812)

	- 这时候才学习了[逆元](https://oi-wiki.org/math/inverse/)，这题用 $O(p)$ 递推求出 $1$ 到 $p-1$ 每个数的逆元

	- 个别数组要开到 $p$ 那么大

### [分块](https://oi-wiki.org/ds/decompose/)

- 2021.05.10 [P4168 [Violet]蒲公英](https://www.luogu.com.cn/problem/P4168)

### [启发式合并](/)

- 2021.06.24 [P3201 [HNOI2009] 梦幻布丁](https://www.luogu.com.cn/problem/P3201)

- 2021.07.01 [[bzoj4919][Lydsy1706月赛]大根堆](https://darkbzoj.tk/problem/4919)

### [主席树/可持久化线段树](/)

- 2021.06.26 [P3834 【模板】可持久化线段树 2（主席树）](https://www.luogu.com.cn/problem/P3834) 这回不是用整体二分做的了
    
- 2021.06.26 [SP1487 Query on a tree III](https://www.luogu.com.cn/problem/SP1487) 求下dfs序就可以套上一题板子了。注意点是点的编号和主席树结点序号不同。。。

- 2021.06.28 [P4197 Peaks](https://www.luogu.com.cn/problem/P4197)
    
- 2021.06.28 [P3402 可持久化并查集](https://www.luogu.com.cn/problem/P3402) 主席树维护历史版本的并查集数组 `fa[]` ，不路径压缩

- 2021.06.30 [P2839 [国家集训队]middle](https://www.luogu.com.cn/problem/P2839)

- 2021.07.01 [Travel To The Ugly](/) 链接先不放了，但ac出的题是真的强

### [线段树合并](/)

- 2021.06.28 [P3521 [POI2011]ROT-Tree Rotations](https://www.luogu.com.cn/problem/P3521)

- 2021.06.28 [P4556 [Vani有约会]雨天的尾巴 /【模板】线段树合并](https://www.luogu.com.cn/problem/P4556)
    
### [三分](/)

- 单峰函数求峰值，可以求导后二分，也可以用三分。

- 2021.07.05 [[十一集训B-day1]tree](http://www.zhengruioi.com/problem/1544) 形如对于若干条直线 $f_i(x)$，在每个 $x$ 取 $F(i)=\max/\min\{f_i(x)\}$，则得到的 $F(i)$ 为一个单峰函数。然后三分求解。

```cpp
while(l<=r){
	ll mid=(r-l)/3,lmid=l+mid,rmid=r-mid;
	ll k1=solve(lmid),k2=solve(rmid);
	if(k1<k2) ans1=lmid,r=rmid-1;
	else ans1=rmid,l=lmid+1;
	ans2=min(ans2,min(k1,k2));
}
```
### [博弈论](http://endless.logdown.com/posts/2014/05/05/find-out-the-winning-strategies-of-the-game-nim-and-grundy-number-notes)

- 2021.07.07 [[ABC206F]Interval Game 2](https://atcoder.jp/contests/abc206/tasks/abc206_f) 第一次写博弈论的题居然还是在VP的时候（~~看了Editorial就AK了~~）

- 2021.08.25 [CF455B A Lot of Games](https://codeforces.com/problemset/problem/455/B)

	- 开始以为就是个 Trie SBT，原来是 SBT 套 SBT。
	
	- 给出的 $k$ 自然是有用的，可以故意输掉第 $k-1$ 局来获得后手换来第 $k$ 局的胜利。

### 数论

- 2021.07.09 [POJ3292 Semi-prime H-numbers](http://poj.org/problem?id=3292) [UVA11105 H-半素数 Semi-prime H-numbers](https://www.luogu.com.cn/problem/UVA11105) 素数、同余

- 2021.07.09 [POJ1061 青蛙的约会](http://poj.org/problem?id=1061) [P1516 青蛙的约会](https://www.luogu.com.cn/problem/P1516) 扩展欧几里得算法

- 2021.07.09 [POJ1845 Sumdiv](http://poj.org/problem?id=1845) [P1593 因子和](https://www.luogu.com.cn/problem/P1593)

	- 挺综合的一道数论题。

	- 运用了唯一分解定理、约束和公式、递归二分求等比数列、快速幂。

- 2021.07.09 [P1495 【模板】中国剩余定理(CRT)/曹冲养猪](https://www.luogu.com.cn/problem/P1495) CRT 板子

- 2021.07.10 [POJ1006 Biorhythms](http://poj.org/problem?id=1006) 运用了CRT

- 2021.07.11 [POJ2115 C Looooops](http://poj.org/problem?id=2115) 扩欧。`long long`类型的要用`1ll<<k`，而不是`1<<k`。

- 2021.07.12 [CF1543A Exciting Bets](https://codeforces.com/contest/1543/problem/A) gcd的一个很trivial但不常用的性质吧，gcd(a,b)=gcd(a-b,b)

### 计数dp

- 2021.07.28 [[ARC112E] Cigar Box](https://atcoder.jp/contests/arc112/tasks/arc112_e) 考虑逆推，结合组合数。

------------

## 题单

### XJ提高过关

CF455B in [博弈论](https://www.wzsyyh.ml/post/oier-note/#%E5%8D%9A%E5%BC%88%E8%AE%BA)

### BZOJ

[#3705 对称的正方形](https://hydro.ac/d/bzoj/p/3705) 二维哈希+二分

### 国家集训队作业

[Link](https://www.wzsyyh.ml/post/team_homework/)

### 思维题

#### 太巧秒了系列

*Problem*

1. [WZOJ#283] 初始在 $0$ 号点，每秒 $\frac{1}{4}$ 概率向左/右移动 $1$ 个单位，$\frac{1}{2}$ 的概率不动。问 $t$ 秒后到达位置 $p$ 的概率。

*Toturial*

1. [WZOJ#283] 将 $1$ 秒延续到 $2$ 秒，每秒 $\frac{1}{2}$ 的概率向左/右移动 $1$ 个单位，与原问题等价。于是答案就是 $\frac{\tbinom{2t}{t+p}}{2^{2t}}$。

#### Level 1

*Problem*

1. [WZOJ#400] 对 $n*n$ 矩阵求满足对任意 $1 \le i,j \le n$ 有 $f_{i,j}=\min ( x_i ,x_j )$ 的排列 $x$ 的个数，并输出字典序最小的一个排列。

1. [WZOJ#403] $n$ 个盘子 $m$ 个柱子的汉诺塔问题，求第 $1$ 个柱子 $n$ 个盘子全移到第 $m$ 个柱子的最小步数。



*Toturial*

1. [WZOJ#400] 找到 $f_{i,j}=n-1$ ，则 $x_i$ 与 $x_j$ 一个为 $n-1$ 一个为 $n$，且第 $i$ 行其余的 $x_k$ 都等于 $f_{i,k}$。

1. [WZOJ#403] 设 $f_{i,j}$ 表示 $i$ 个盘子 $j$ 个柱子的最小步数，显然有 $f_{i,j}=\min \{ 2 \times f_{k,j} + f_{i-k,j-1} \}$

#### Level 2

*Problem*

1. [WZOJ#227] 维护一个长度为 $n$ 的序列，要求：1.单点修改。2.区间查询是否存在区间内三个数构成三角形并求周长最大的可能值。

*Toturial*

1. [WZOJ#227] 通过类似斐波那契的数列发现，只用考虑前 $50$ 大的数。数据结构再维护一下。

## 「实时更新」查漏补缺

- 2021.03.05 [离散化](https://www.luogu.com.cn/blog/wzsyyh/clbq-lsh)

- 2021.03.16 准备系统学字符串算法

- 2021.03.17 老惨了发现虚树已经忘了无数遍了。。。[板子集合](https://www.luogu.com.cn/blog/wzsyyh/banzi)

## 成就

- 2021.10.06 由于 ss 催更，更一发吧。

![](/image/20211006ss.png)

![](/image/the-first-time-to-get-rk1.png)

第一次拿榜1也挺惊喜的其实。

- 2021.10.17

![](/image/20211017.png)

第二次拿榜一也挺惊喜的其实。

- 2021.10.18

惊喜的发现：

![](/image/20211018rank2.png)

然而：

![](/image/20211018zr.png)

## 一些题

### 2020tg10

*day1*

A. 把 $n$ 划分成尽量少的数字之和，每个数都形如 $3k^3 - 3k +1 (k\ge 1)$。

B. 求给定字符串中 $AA^rA$ 串的数量（其中 $A^r$ 表示 $A$ 的反串）。

*Tutorial*

A. mod 3 之后是结论题。

B. 先 Manacher，再在树状数组中找满足 $i-man_i \le j$ 的 $j$ 的数量，再把 $i$ 加入到树状数组中。
