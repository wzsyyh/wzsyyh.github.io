---
title: 「题解」[NOIP2017 提高组] 列队
date: 2021-06-25 13:54:40
tag: [题解, 数据结构, 平衡树]
category: 题解
---
## 思路

“向左看齐”和“向前看齐”这两条指令，相当于在序列中删除一个元素并维护行、列中的相对顺序。

由于此题是教练给出的平衡树习题，想到用平衡树来维护所谓的序列。

对每一行开一棵平衡树，删除 $(x,y)$ 相当于在第 $x$ 行的平衡树中删除第 $y$ 个元素。在删除之后，我们发现这一行已经“向左看齐”了。

那么怎么做到“向前看齐”呢？在“向左看齐”之后，缺人的位置一定在最后一列，也就是说，只有最后一列才会因“向前看齐”而改变。想到对最后一列另外开一棵平衡树。对于删除 $(x,y)$ 操作，在最后一列的这棵平衡树上删除第 $x$ 个 元素，再把之前第 $x$ 行删除的第 $y$ 个元素加到这棵平衡树的末端。

## 实现

这里用 Splay 实现

对于每 $i$ 行，建一棵平衡树标号为 $i$

对于第 $m$ 列，建一棵平衡树标号为 $0$

对于每一次操作：

1. 删除第 $0$ 棵平衡树中第$i$个元素
2. 删除第 $i$ 棵平衡树中第$j$个元素
3. 在第 $0$ 棵平衡树末端插入在 2. 中删除的元素

这样做的原因：

1. 在第 $0$ 棵平衡树中删除元素，实现了“向前看齐”
2. 在第 $i$ 棵平衡树中删除元素，实现了“向左看齐”
3. 在第 $0$ 棵平衡树末插入元素，实现了“学生归队”

另外，**如果对于每一个元素我们都建立了一个结点的话，会有大量多余的空间开销**。因为有很多连在一起的元素自始至终都没有分开，我们将区间存在一个结点中，当用到这个区间中的一个结点时再考虑对区间拆分为两个结点。

## CODE

```cpp
#include <bits/stdc++.h>
#define int long long
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

const int N=3e6+5;
int n,m,q,a[N],tot;
int sz[N],ch[N][2],val[N][2],fa[N];

struct Splay{

	int rt;

    inline void push(int x){
        sz[x]=sz[ch[x][0]]+sz[ch[x][1]]+val[x][1]-val[x][0]+1;
    }

	inline bool wrt(int x){return x==ch[fa[x]][1];}
	inline void rotate(int x){
	    int p=fa[x],g=fa[p],k=wrt(x),b=ch[x][k^1];
	    ch[p][k]=b,fa[b]=p;
	    ch[g][wrt(p)]=x,fa[x]=g;
	    ch[x][k^1]=p,fa[p]=x;
	    push(p),push(x);
	}
	
	inline void splay(int x,int tar=0){
	    while(fa[x]!=tar){
	        if(fa[fa[x]]!=tar)
	            wrt(x)==wrt(fa[x])?rotate(fa[x]):rotate(x);
	        rotate(x);
	    }
	    if(!tar) rt=x;
	}

    inline int kth(int k){
        int x=rt;
        while(1){
            if(ch[x][0] && k<=sz[ch[x][0]]) x=ch[x][0];
            else if(ch[x][1] && k>sz[x]-sz[ch[x][1]]) k-=sz[x]-sz[ch[x][1]],x=ch[x][1];
            else {
                k-=sz[ch[x][0]];
                if(k!=1){
                    fa[ch[++tot][0]=ch[x][0]]=tot,fa[ch[x][0]=tot]=x;
                    val[tot][0]=val[x][0],val[tot][1]=val[x][0]+k-2,val[x][0]=val[tot][1]+1;
                    push(tot);
                    k=1;
                }
                if(k!=val[x][1]-val[x][0]+1){
                    fa[ch[++tot][1]=ch[x][1]]=tot,fa[ch[x][1]=tot]=x;
                    val[tot][1]=val[x][1],val[tot][0]=val[x][0]+k,val[x][1]=val[tot][0]-1;
                    push(tot);
                }
                return x;
            }
        }
    }

    inline int newNode(int l,int r){
        int x=++tot;
        ch[x][0]=ch[x][1]=fa[x]=0;
        val[x][0]=l,val[x][1]=r;
        sz[x]=r-l+1;
        return x;
    }

    inline int build(int l,int r){
        if(l>r) return 0;
        int mid=l+r>>1,x=newNode(a[mid],a[mid]);
        if(l==r) return x;
        if(ch[x][0]=build(l,mid-1)) fa[ch[x][0]]=x;
		if(ch[x][1]=build(mid+1,r)) fa[ch[x][1]]=x;
        push(x);
        return x;
    }

    inline void join(int u,int v){
        fa[u]=0,fa[v]=0;
        int w=u;
        while(ch[w][1]) w=ch[w][1];
        splay(w);
        ch[w][1]=v,fa[v]=w;
        push(w);
    }

    inline int pop(int k){
        int x=kth(k);
        splay(x);
        if(!ch[x][0] || !ch[x][1])
            fa[rt=ch[x][0]|ch[x][1]]=0;
        else join(ch[x][0],ch[x][1]);
        return val[x][0];
    }

    inline void push_back(int v){
        int x=newNode(v,v);
        if(!rt) rt=x;
        else {
            int w=rt;
            while(ch[w][1]) w=ch[w][1];
            splay(w);
            ch[w][1]=x,fa[x]=w;
            push(w);
        }
    }

}s[N];

/*
对于每i行，建一棵平衡树标号为i
对于第m列，建一棵平衡树标号为0

对于每一次操作：
1. 删除第0棵平衡树中第i个元素
2. 删除第i棵平衡树中第j个元素
3. 在第0棵平衡树末端插入在2.中删除的元素

这样做的原因：
1. 在第0棵平衡树中删除元素，实现了“向前看齐”
2. 在第i棵平衡树中删除元素，实现了“向左看齐”
3. 在第0棵平衡树末插入元素，实现了“学生归队”
*/

signed main(){
//	freopen("1.in","r",stdin);
//	freopen("my.out","w",stdout);
    n=gin(),m=gin(),q=gin();
    for(int i=1;i<=n;i++){
        s[i].rt=s[i].newNode((i-1)*m+1,i*m-1);
        a[i]=i*m;
    }
	s[0].rt=s[0].build(1,n);
    while(q--){
        int x=gin(),y=gin(),z;
	   	s[x].push_back(s[0].pop(x));
	    printf("%lld\n",z=s[x].pop(y));
        s[0].push_back(z);
    }
    return 0;
}

```