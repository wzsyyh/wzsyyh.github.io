---
title: 「题解」[NOI2007] 货币兑换(Cash) 笔记
date: 2021-05-30 22:00:05
tag: [题解, 数据结构, 技巧]
category: 题解
---
> upd 2021.6.4:之前一直以为这题是cdq分治在斜率优化dp中的一个应用，今天看陈丹琦的论文《从《Cash》谈一类分治算法的应用》才知道这题就是cdq分治起源

参考了[这篇题解](https://www.luogu.com.cn/blog/riverhamster/solution-p4027)的思路

## 思路
### 贪心
首先很容易贪心的想到，最优的情况肯定是“买的时候把钱花完、卖的时候把券卖完”。
### 推dp式
记第 $i$ 天结束时最大的钱数为 $f_i$
考虑通过输入给出的每组 $A_i,B_i,R_i$ ，计算出第 $i$ 天结束时所能买到的两种券的个数
$$ x_i=f_i \frac{R_i}{A_i R_i+B_i} $$
$$ y_i=f_i \frac{1}{A_i R_i+B_i} $$
则有转移方程
$$ f_i=\max \{f_{i-1},{\max \{x_j A_i+y_j B_i\}}\} $$
转移到 $i$ 时，决策 $j_1$ 比 决策 $j_2$ （其中 $j_1<j_2$ ）优等价于
$$ \frac{y_{j_1}-y_{j_2}}{x_{j_1}-x_{j_2}} > -\frac{A_i}{B_i} $$
不同于平常的斜率优化dp，这时推出来的斜率不是一个定值。但如果在计算 $i$ 时已经计算完成了 $1$ 到 $i-1$ ，就可以用斜率优化了。于是想到了cdq分治。
### cdq分治

考虑cdq分治传统步骤
1. cdq(l,mid)
1. 计算当前左半区间修改对右半区间询问的贡献
1. cdq(mid+1,r)

考虑 2. 具体怎么做：按 $-\frac{A_i}{B_i}$降序排序来保证之后查询凸壳时的复杂度。扫一遍左半部分，用单调队列的右指针维护上凸包（因为要使得斜率只降不升）；扫一遍右半部分，每次移动左指针来更新当前最优的决策点。

由于分治递归左右区间的时候要保证时间是对的，递归之前要把左右区间区分开。

## CODE
```cpp
#include <bits/stdc++.h>
#define max(a,b) a>b?a:b
using namespace std;
inline int gin(){
    int s=0,f=1;
    char c=getchar();
    while(c<'0' || c>'9'){
        if(c=='-') f=-1;
        c=getchar();
    }
    while(c>='0'&&c<='9'){
        s=(s<<3)+(s<<1)+(c^48);
        c=getchar();
    }
    return s*f;
}

const int N=1e5+5,inf=1e9;
int st[N],n;
double A[N],B[N],R[N],f[N],s;

struct node{
    int id;
    double x,y;
}t[N],tmp[N];
inline bool cmp(node a,node b){
    return -(A[a.id]/B[a.id]) > -(A[b.id]/B[b.id]);
}

double slope(int x,int y){
    if(t[x].x==t[y].x) return inf;
    return (t[y].y-t[x].y)/(t[y].x-t[x].x);
}

void cdq(int l,int r){
    if(l==r){
        f[l]=max(f[l],f[l-1]);
        t[l].x=f[l]/(A[l]*R[l]+B[l])*R[l];
        t[l].y=f[l]/(A[l]*R[l]+B[l]);
        return;
    }
    int mid=l+r>>1,p=l,q=mid+1;
    for(int i=l;i<=r;i++){//递归前需把左右区间区分开
        if(t[i].id<=mid) tmp[p++]=t[i];
        else tmp[q++]=t[i];
    }
    for(int i=l;i<=r;i++) t[i]=tmp[i];
    cdq(l,mid);
    q=0,p=1;
    for(int i=l;i<=mid;i++){//维护上凸包
        while(q>1 && slope(st[q-1],st[q])<slope(st[q],i)) q--;
        st[++q]=i;
    }
    for(int i=mid+1;i<=r;i++){
        while(p<q && slope(st[p],st[p+1])>-A[t[i].id]/B[t[i].id]) p++;//查询凸壳。如果没有预先按-A[i]/B[i]排序，这里每次二分查询是log的
        f[t[i].id]=max(f[t[i].id],t[st[p]].x*A[t[i].id]+t[st[p]].y*B[t[i].id]);
    }
    cdq(mid+1,r);
    p=l,q=mid+1;
    for(int i=l;i<=r;i++){
        if(q>r || p<=mid && t[p].x<t[q].x) tmp[i]=t[p++];
        else tmp[i]=t[q++];
    }
    for(int i=l;i<=r;i++) t[i]=tmp[i];
    return;
}

signed main(){
    n=gin();
    scanf("%lf",&s);
    for(int i=1;i<=n;i++){
        scanf("%lf%lf%lf",&A[i],&B[i],&R[i]);
        double x=s/(A[i]*R[i]+B[i])*R[i];
        double y=s/(A[i]*R[i]+B[i]);
        t[i]=(node){i,x,y};
        f[i]=s;
    }
    sort(t+1,t+n+1,cmp);
    cdq(1,n);
    printf("%.3lf\n",f[n]);
    return 0;
}
```

