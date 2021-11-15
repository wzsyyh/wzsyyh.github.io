---
title: 集训队作业做题记录
date: 2021-10-19 15:00:16
tag: 学习笔记
category: 学习笔记
---

> ljc1301 跟 Owen_codeisking 都有推荐做集训队作业，于是决定挑战一下自己。

## IOI2020国家集训队作业

### [CF504E Misha and LCP on Tree](https://codeforces.com/problemset/problem/504/E)

*AC on 2021.10.19 [CODE](/post/code/#CF504E)*

看道题就想到树链剖分，结合一下哈希，联系一下二分。好像也是我第一次写双模数哈希（因为Codeforces卡`unsigned`来着）。

于是得到了：

![](/image/CF504E.png)

~~就这？~~ 就这样我创建了这个页面。

### [CF547D Mike and Fish](https://codeforces.com/problemset/problem/547/D)

*AC on 2021.10.20 [CODE](/post/code/#CF547D)*

昨天ZROI模拟赛刚做了一道给边染色的题，而这题不过是改成了给点染色，今天ZROI模拟赛刚做了一道巧妙转换成二分图染色的题。那么这题完完全全就像是那两道题综合一下的题，难度并没有很大，不过可惜的是还是没有自己独立思考出来。

对于每一个横/纵坐标上的点，每两个一组连边，之后跑二分图染色。同一组的两个点颜色不同，保证了同一行/列两种颜色之差不超过 $1$，每个点最多连 $2$ 条边，故要么是链要么是 $4$ 个点的环（不是奇环）。

### [CF527E Data Center Drama](https://codeforces.com/problemset/problem/527/E)

*AC on 2021.10.20 [CODE](/post/code/#CF527E)*

ljc：我们看看谁先过掉这题。

晚饭前我们俩都*TLE on Test #36*，他晚上去数竞那边了，于是我先过了这题！

TLE的原因是欧拉回路每条边没有保证只dfs到一遍，应当将 `for(int i=head[u];i;i=ne[i])` 改成 `for(int& i=head[i];i;i=ne[i])`。

**发现自己对欧拉回路的理解非常的错误！！！ljc提醒后才明白建那个栈的意义所在！！！我先前一直以为那个栈只是为了记录下一个欧拉回路，然而这是欧拉回路的关键！**

结合ZROI昨天和今天的T2，可以做掉上面那道[CF547D](/post/team_homework/#CF547D-Mike-and-Fish)，再结合上面这题，可以做掉这题。我这个作业顺序非常正确。
