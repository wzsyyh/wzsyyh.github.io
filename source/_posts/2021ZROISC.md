---
title: 「游记」2021ZROISC
date: 2021-07-16 16:01:28
tag: 游记
category: 游记
---

## Day 0

2021.07.16 中午到了金华。

中午川菜辣死了，下午麦当劳冰淇淋有亿点小。

## Day 1

刚AK IOI2021的dls在隔壁桌吃早餐。

现在我们楼下都是NOI赛前集训的神佬们，有dls、lk……

再想想自己生在浙江，不禁流下了眼泪。

南外的吕秋实吕老师！

讲的大部分东西都很熟，只有欧拉序+RMQ求LCA之前没有写过，写了以后发现虽然是 $O(1)$ 询问，但板子题比树剖还是要慢。

例题列表

T1 https://atcoder.jp/contests/abc070/tasks/abc070_d ✔️

T2 树上路径不带修最小值 ✔️

T3 https://codeforces.ml/contest/609/problem/E ✔️

T4 https://acm.hdu.edu.cn/showproblem.php?pid=3183 ✔️

T5 http://poj.org/problem?id=3419 ✔️

T6 https://codeforces.ml/contest/1301/problem/E ✔️

T7 https://codeforces.ml/problemset/problem/1527/D ✖️

T8 https://www.luogu.com.cn/problem/UVA1707 

## Day 2

讲线段树和树状数组的时候感觉还是很水，然后：“现在我们已经学会线段树了，快来看一下这道题吧。”于是暴毙了。
今天的题还是蛮难的吧。

T1 求给定序列冒泡排序需要交换多少次（求逆序对） ✔️

T2 https://www.luogu.com.cn/problem/P4868  ✔️

T3 http://poj.org/problem?id=2155 ✔️

T4 https://codeforces.ml/contest/1527/problem/E ✖️

T5 从区间拓展到树上http://poj.org/problem?id=3728 ✔️

T6 http://acm.hdu.edu.cn/showproblem.php?pid=6315 ✔️ [笔记](/post/hdu6315)

T7 http://acm.hdu.edu.cn/showproblem.php?pid=5634

T8 https://codeforces.com/contest/1149/problem/C

## Day 3

第一场模拟赛，太惨烈了不想记录

T1的`freopen`忘记去掉了，抱灵了

T2开始题意理解错了，写了个 Kruskal ，只得了10分。看数据范围应该想到状压。

T3可以转化为求每个点开头的最长上升子序列、最长下降子序列，还要求计数。

用树状数组计数较为方便：

```cpp
inline void add(int x,int d,int num){
    while(x<=n+1){
        if(c1[x]<d) c1[x]=d,c2[x]=num;
        else if(c1[x]==d) (c2[x]+=num)%=mod;
        x+=x&-x;
    }
}

pi sum(int x){
    pi res=make_pair(0,0);
    while(x>0){
        if(c1[x]>res.first){
            res.first=c1[x];
            res.second=c2[x];
        }
        else if(c1[x]==res.first) (res.second+=c2[x])%=mod;
        x-=x&-x;
    }
    return res;
}
```

## Day 4

https://vjudge.net/contest/447983:

T1 https://acm.hdu.edu.cn/showproblem.php?pid=6638 ✔️

T2 https://acm.hdu.edu.cn/showproblem.php?pid=6606 ✔️

T3 https://acm.hdu.edu.cn/showproblem.php?pid=6609 ✔️

T4 https://www.luogu.com.cn/problem/CF600E dsu on tree✔️ 线段树合并✖️

T5 https://www.luogu.com.cn/problem/P3521 ✔️吃老本

T6 https://www.luogu.com.cn/problem/P4556 ✔️吃老本

T7 https://codeforces.com/problemset/problem/1181/D ✔️

T8 https://codeforces.com/problemset/problem/1354/D ✔️on 2021.10.3

## Day 5

https://vjudge.net/contest/448336

T1 https://www.luogu.com.cn/problem/CF955D ✔️

T2 https://www.luogu.com.cn/problem/CF985F ✔️

T3 https://darkbzoj.tk/problem/2462 ✔️on 2021.10.3

T4 https://www.luogu.com.cn/problem/UVA1519 ✔️on 2021.10.3

T5 https://www.luogu.com.cn/problem/P4052 ✔️

T6 https://vjudge.net/problem/HihoCoder-1877 hihocoder ✔️on 2021.10.3（这个OJ似乎爆了交不了）

T7 https://acm.hdu.edu.cn/showproblem.php?pid=3336 ✔️

T8 https://www.luogu.com.cn/problem/UVA10298 ✔️吃老本

T9 https://www.luogu.com.cn/problem/P3435 ✔️吃老本

T10 http://poj.org/problem?id=2752 ✔️

T11 https://www.luogu.com.cn/problem/P2375 ✔️吃老本

T12 https://www.luogu.com.cn/problem/P4600 ✔️

## Day 6

依然是字符串 https://vjudge.net/contest/448336

扩展kmp

T1 https://acm.hdu.edu.cn/showproblem.php?pid=2594 ✔️

T2 https://acm.hdu.edu.cn/showproblem.php?pid=6629 ✔️

马拉车拉马

T3 https://codeforces.com/gym/101981/attachments

T4 https://www.luogu.com.cn/problem/P3454

## Day 7

21 暑期集训C班 day2

T1 贪心sbt。

T2 自己脑残加了些特判来优化，爆了。还有就是0+没有特判。

T3 写了二分+二分，O(qlognlogm)，还算得了个80分吧。

艹，已经很接近正解了。。。

我的二分+二分相当于两次二分出 $i$ 和 $j$ ，看是否满足 $i+j=\frac{n}{2}$ 。

其实只用一次二分 $i$ ，看 $\frac{n}{2}-i$ 是否在另一个序列中。

T4 正解显然是 AC自动机+数位dp ，然而数位dp写炸了，最后想交个暴力结果暴力也挂了，抱灵了。

$f[statu][i][0/1][0/1][bin]$

有关中位数的题1 https://www.luogu.com.cn/problem/AT2165

二分答案mid，最下面一行大于 $mid$ 设为 $1$ ，小于 $mid$ 设为 $0$ 。

有关中位数的题2 https://acm.ecnu.edu.cn/problem/3681/

二分一个 $mid$ ，大于 $mid$ 的设为 $1$ ，小于 $mid$ 的设为 $-1$ ，按拓扑序dp求最长路看是否大于 $0$ 。

## Day 8

https://www.luogu.com.cn/problem/P3350 ✔️on 2021.10.6

https://www.luogu.com.cn/problem/SP2371 ✔️

https://acm.hdu.edu.cn/showproblem.php?pid=6800

https://www.luogu.com.cn/problem/P5163

https://www.luogu.com.cn/problem/CF1365G

## Day 9

各品种平衡树

https://www.luogu.com.cn/problem/P1486 ✔️

https://www.luogu.com.cn/problem/P2161 ✔️on 2021.10.7

https://www.luogu.com.cn/problem/P2521

https://www.luogu.com.cn/problem/P3224


## Day 10

可持久化数据结构

### 例题

https://codeforces.com/contest/323/problem/C

https://loj.ac/p/2718

https://loj.ac/p/3048

https://loj.ac/p/2555

https://loj.ac/p/3346

https://www.luogu.com.cn/problem/P2839

http://acm.hdu.edu.cn/showproblem.php?pid=5756

http://acm.hdu.edu.cn/showproblem.php?pid=5118

https://codeforces.com/contest/1340/problem/F

### 课后练习

https://loj.ac/p/2551

https://uoj.ac/problem/29

https://loj.ac/p/2310

https://codeforces.ml/contest/702/problem/F

## Day 11

### 例题

https://www.luogu.com.cn/problem/P2408

https://codeforces.ml/contest/1073/problem/G

https://codeforces.ml/contest/232/problem/D

https://codeforces.ml/contest/666/problem/E

https://onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=1770

https://loj.ac/p/2083

https://codeforces.ml/contest/1063/problem/F

课后练习

http://poj.org/problem?id=3581

https://loj.ac/p/2133

https://loj.ac/p/2073

https://loj.ac/p/3326

## Day 12

Class B **DP**

### 例题

https://www.luogu.com.cn/problem/P1896

https://codeforces.ml/problemset/problem/1238/E

https://www.luogu.com.cn/problem/P4127

https://loj.ac/p/6770

https://www.luogu.com.cn/problem/P1850

https://codeforces.com/gym/101623/problem/E

https://codeforces.ml/problemset/problem/1237/F

https://atcoder.jp/contests/arc112/tasks/arc112_e

http://poj.org/problem?id=1769

https://acm.hdu.edu.cn/showproblem.php?pid=6856

https://codeforces.ml/contest/1322/problem/D

https://www.luogu.com.cn/problem/P3628

https://loj.ac/p/2249

https://acm.hdu.edu.cn/showproblem.php?pid=6065

https://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=2591

### 课后练习

https://codeforces.ml/contest/1106/problem/E

https://loj.ac/p/2540

https://atcoder.jp/contests/dp/tasks/dp_y

https://atcoder.jp/contests/dp/tasks/dp_w

https://www.luogu.com.cn/problem/P2612

https://www.luogu.com.cn/problem/P4027

## Day 13

Class B **字符串**

### 例题

https://acm.hdu.edu.cn/showproblem.php?pid=2609

https://www.luogu.com.cn/problem/P4287

https://www.luogu.com.cn/problem/P5446

https://www.luogu.com.cn/problem/P2375

https://loj.ac/p/3103

https://codeforces.ml/contest/1466/problem/G

https://www.luogu.com.cn/problem/P2414

https://codeforces.com/contest/697/problem/F

http://opentrains.snarknews.info/~ejudge/team.cgi?SID=92517543ff8190b4&action=2&lt=1

几道 NFLS 的题

https://www.luogu.com.cn/problem/P3975

https://loj.ac/p/3326

https://codeforces.ml/contest/700/problem/E

https://ioihw20.duck-ac.cn/problem/261

### 课后习题

https://www.luogu.com.cn/problem/P3181

http://codeforces.ml/contest/666/problem/E

https://loj.ac/p/2720

https://codeforces.ml/problemset/problem/1037/H

https://vjudge.net/problem/TopCoder-10413

https://vjudge.net/problem/CodeChef-DIFTRIP

## Day 14

Class B

一堆数论题

## Day 15

Class B

一堆数学题

## Day 16

Class B

亦可赛艇ACM赛 QwQ

学军的sbb 和 人大附的zxh 也带不动我。。。最终 $2$ 个气球，还不够平分。

## Day 17

Class C **网络流和二分图**

例题大都是 *网络流 24 题* 中的。

## Day 18

Class C **%你赛**

## Day 19

Class C **%你赛**

## Day 20

Class C **区间dp 树形dp**

## Day 21

Class C **状压dp**

## Day 22

Class C **%你赛**

今天的比赛出了点情况。

考试时我对 T2 有点疑问，询问了出题人题意。在回答之前我按自己的理解交了一发。得到回答后我改了一版交了一发。

然而考后前一发过了，后一发则获得 $0$ 分好成绩。

我找出题人老师讨公道，想要搞回属于我的 $100$，~~毕竟还要计 Rating~~。

“诶你这个为什么对？跟 std 是等价的吗？”“诶我这个为什么对？”

于是老师发现 T2 实际上是 **NP Hard** 问题。所有人 T2 清零计 Rating。

虽然我把跟我一样的那些一直死磕 T2 的人一起搞没了，但我获得了出题人老师的一个 23.33RMB 的红包！

不亏。

## Day 23

Class C

> 数位dp    ✖️
> 
> 集合幂级数    ✔️

把强少的 `集合幂级数.md` ~~不要脸地~~转载到了我的博客上。

## Day 24

Class C **计数与期望dp**

今天课好像没啥好记录的。晚上 CF 只过了 2 题 ~~离 Specialist 还差8分~~。

## Day 25

Class C **dp优化**

xtq 激情演唱《水手》，wzy 精彩呈现《十年》。

我以为学过了决策单调性、斜率优化就可以听得轻松了，然而 wzy 大部分时间在讲其他的优化方法。

wqs 二分、长链剖分，还算写过、听得懂。有人想听 分治FFT优化，于是 wzy 开始讲 GF。然后就断线并重连失败了。

## Day 26

Class B **%你赛**

B 题忘了取模直接少了 60 分 QwQ。

要是记得取模了，这在 AB 模拟赛算不错了的吧。

## Day 27

Class C **%你赛**

正睿经典普及，挂挺惨的 QwQ。

## Day 28

Class C **数论**

莫比乌斯反演题做爽起来了。

楼上 AB 唱歌狂欢了。

## Day 29

Class C **线性代数**

虽然 wzy 觉得讲的东西很简单，但我还是掉线了。。。

## Day 30

Class C **%你赛**

最后一天，模拟赛还算收场收的好吧，280pts，Rank 4。虽然前两题完全送分的，但还是有人做不出来或是做得慢给我把排名整上去了![](//啧.tk/kk)

### 前三不在现场，我被抓上去唱歌？

与 wzy哥哥 合唱了《花海》。先前没人好意思上来唱歌，我开了这先河之后就陆续有人踊跃参加了。

### 离开

这 30 天，感谢有py一中的闫神、徐神、黄神、潘神的陪伴。他们同学四人将原本落单的我当做亲同学一般看待。这一别，很可能是永别，而这段经历，也许是我们求学路上最难忘的一段经历吧。

感谢权贵学校学子——人大附中的zxh与学军的sbb带我打 ACM亦可赛艇杯。

上午爸妈就到了，中午带我去了那 ACM前三的队伍送的烤肉券 的烤肉店吃午餐，下午讲完题唱完歌就回 WZ 了。明早就回 WZHS 了。

最后我想用所有OIer们入门时的第一个程序的输出，打开明天崭新的世界。

```
Hello World!
```