---
title: 「学习笔记」树上差分
date: 2021-06-28 16:30:46
tag: [技巧]
category: 学习笔记
---
问了 [阿丑](https://www.luogu.com.cn/user/364963) 两道题的询问操作部分，发现我两次问的东西是一模一样的东西：树上差分。

一道是主席树题[P3302 [SDOI2013]森林](https://www.luogu.com.cn/problem/P3302)，一道是线段树合并[P4556 [Vani有约会]雨天的尾巴 /【模板】线段树合并](https://www.luogu.com.cn/problem/P4556)

对 $x$ 到 $y$ 路径上的点进行操作时，找到 $lca$ 和 $fa[lca]$ 。这里不妨操作是 $+val$

![](file://C:/Users/wzsyy/Documents/Gridea/post-images/1625312990231.png)

类似于差分数组的操作，对 $x$ 和 $y$ 进行 $+val$ ，对 $lca$ 和 $fa[lca]$ 进行 $-val$ 。然后再 `pushup` 上传结点信息。

 _下图中**浅蓝色**的“+1”表示 `pushup` 时通过边传递上来的信息_ 

![](file://C:/Users/wzsyy/Documents/Gridea/post-images/1625313006333.png)

这样一来 $x$ 与 $y$ 实现了 $+1$ ，$lca$ 实现了 $+1+1-1=+1$ ，$fa[lca]$ 实现了 $+1-1=0$ 。

[P3302 [SDOI2013]森林](https://www.luogu.com.cn/problem/P3302)一题中的：

```cpp
int query(int x,int y,int p1,int p2,int l,int r,int k){
    int mid=l+r>>1;
    int lsz=sum[lc[x]]+sum[lc[y]]-sum[lc[p1]]-sum[lc[p2]];//就是这句！
    if(l==r) return b[l];
    if(k<=lsz)
        return query(lc[x],lc[y],lc[p1],lc[p2],l,mid,k);
    else return query(rc[x],rc[y],rc[p1],rc[p2],mid+1,r,k-lsz);
}

main函数中询问操作的回答↓
query(rt[x],rt[y],rt[yyh],rt[st[yyh][0]],1,len,k);
```

以及[P4556 [Vani有约会]雨天的尾巴 /【模板】线段树合并](https://www.luogu.com.cn/problem/P4556)一题中的：

```cpp
mian函数里↓
rt[x[i]]=upd(rt[x[i]],1,len,z[i],1);
rt[y[i]]=upd(rt[y[i]],1,len,z[i],1);
rt[yyh]=upd(rt[yyh],1,len,z[i],-1);
if(fa[yyh]) rt[fa[yyh]]=upd(rt[fa[yyh]],1,len,z[i],-1);

//之后有merge操作合并每个点与它儿子的权值线段树，实现了差分标记的上传
```

由于只是给自己留的一个记录，所以写的非常简略且例子也不是经典的树上差分例子。