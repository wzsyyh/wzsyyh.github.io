---
title: 「学习笔记」Splay
date: 2021-02-19 14:31:34
tag: [数据结构, 平衡树]
category: 学习笔记
---
upd 2021.6.10:添加了[P6136 【模板】普通平衡树（数据加强版）](https://www.luogu.com.cn/problem/P6136)的实现

## (1)Rotate(x)

将 $x$ 向上移动一级，并将 $fa[x]$ 作为儿子，保持 $BST$ 的性质。

```cpp
inline void Rotate(const int &x){//旋转 
    int y=fa[x],z=fa[y]; 
	int b=(lc[y]==x)?rc[x]:lc[x];
	fa[x]=z,fa[y]=x;
	if(b)fa[b]=y;
	if(z)(y==lc[z]?lc[z]:rc[z])=x;
	if(x==lc[y])rc[x]=y,lc[y]=b;
	else lc[x]=y,rc[y]=b;
}
```

## (2)Splay(x,target)

将伸展树中节点 $x$ 调整为 $target$ 的儿子。是伸展树的核心。

- 如果爷爷是 $target$，单旋一次
- 如果爷爷不是 $target$ 且父亲和爷爷方向一致，先旋父亲再旋自己
- 如果爷爷不是 $target$ 且父亲和爷爷方向不同，旋两次自己

```cpp
inline bool Wrt(const int &x){//判断x是否为父亲的右儿子 
	return rc[fa[x]]==x;
}
inline void Splay(const int &x,const int &tar){//调整 
	while(fa[x]!=tar){
		if(fa[fa[x]]!=tar)
			Wrt(x)==Wrt(fa[x])?Rotate(fa[x]):Rotate(x);
		Rotate(x);
	}
	if(!tar)rt=x;
}
```

## (3)Find(v)

```cpp
inline int Find(int v){
	int x=rt;
	while(x){
		if(v==val[x])break;
		if(v> val[x])x=rc[x];
		else x=lc[x];
	}
	if(x)Splay(x,0);
	return x;
}
```

## (4)Insert(v)

```cpp
inline void Insert(int v){//插入 
	int x=rt,y=0,lr;
	while(x){
		++sz[y=x];
		if(v<val[x])lr=0,x=lc[x];
		else lc=1,x=rc[x];
	}
	x=++tot;
	fa[x]=y,val[x]=v,sz[x]=1;
	if(y)(lr==0?lc[y]:rc[y])=x;
	Splay(x,0);
}
```

## (5)Join(u,v)

```cpp
inline void Join(int u,int v){//合并 
	fa[u]=fa[v]=0;
	int w=u;
	while(rc[w])w=rc[w];
	Splay(w,0);
	rc[w]=v,fa[v]=w;
}
```

## (6)Delete(u)

```cpp
inline void Delete(int u){//删除 
	Splay(u,0);
	if(!lc[u] || !rc[u])
		fa[rt=lc[u]+rc[u]]=0;
	else Join(lc[u],rc[u]);
	lc[u]=rc[u]=0;
}
```

## (7)GetRank(v)

排名可表示为左子树大小+1

```cpp
inline int GetRank(int v){//查询排名 
	int x=Find(v);
	return sz[lc[x]]+1;
}
```

## (8)Spilt(v)

以元素 $v$ 所在的节点 $x$ 为界，将伸展树分为左右两颗

首先执行 `Find(v)` ，再 `Splay(x,0)` ，最后 $x$  的左子树为 $S1$ ，右子树为 $S2$

### 其他

除了上述8种基本操作，伸展树还支持求前驱、后继、最值、排名第k的元素等操作

upd:2021.4.27 [P3369 【模板】普通平衡树](https://www.luogu.com.cn/problem/P3369)

```cpp
#include <bits/stdc++.h>
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

const int N=1e6+5;
int n,fa[N],lc[N],rc[N],val[N],sz[N],rt,tot,cnt[N];

inline void push(int x){
	if(x){
		sz[x]=cnt[x];
		if(lc[x]) sz[x]+=sz[lc[x]];
		if(rc[x]) sz[x]+=sz[rc[x]];
	}
	return;
}
inline bool get(int x){
	return x==rc[fa[x]];
}
inline void clear(int x){
	lc[x]=rc[x]=fa[x]=val[x]=sz[x]=cnt[x]=0;
}

void rotate(int x){
	int y=fa[x],z=fa[y];
	int b=lc[y]==x ? rc[x] : lc[x];
	fa[x]=z,fa[y]=x;
	if(b) fa[b]=y;
	if(z) (lc[z]==y ? lc[z] : rc[z])=x;
	if(x==lc[y]) rc[x]=y,lc[y]=b;
	else lc[x]=y,rc[y]=b;
	push(x);
	push(y);
}

void splay(int x,int tar=0){
	while(fa[x]!=tar){
		if(fa[fa[x]]!=tar)
			get(x)==get(fa[x]) ? rotate(fa[x]) : rotate(x);
		rotate(x);
	}
	if(!tar) rt=x;
}

inline int find(int v){
	int x=rt;
	while(x){
		if(val[x]==v) break;
		if(val[x]> v) x=lc[x];
		else x=rc[x];
	}
	if(x) splay(x);
	return x;
}

inline void ins(int v){
	int w=find(v);
	if(w){
		cnt[w]++;
		return;
	}
	int x=rt,y=0,dir;
	while(x){
		++sz[y=x];
		if(v<val[x]) x=lc[x],dir=0;
		else x=rc[x],dir=1;
	}
	x=++tot;
	fa[x]=y,val[x]=v,sz[x]=1,cnt[x]=1;
	if(y) (dir==0 ? lc[y] : rc[y])=x;
	push(y);
	splay(x);
}

inline int rk(int v){
	int x=find(v);
	return sz[lc[x]]+1;
}

inline int kth(int k){
	int x=rt,y=k;
	while(x){
		if(y<=sz[lc[x]])
			x=lc[x];
		else {
			y-=sz[lc[x]]+cnt[x];
			if(y<=0){
				splay(x);
				return val[x];
			}
			x=rc[x];
		}
	}
}

inline void join(int u,int v){
	fa[u]=fa[v]=0;
	int w=u;
	while(rc[w]) w=rc[w];
	splay(w);
	rc[w]=v,fa[v]=w;
}

inline void del(int v){
	int x=find(v);
	if(cnt[x]>=2){
		cnt[x]--;
		push(x);
		return;
	}
	if(!lc[x] || !rc[x])
		fa[rt=lc[x]|rc[x]]=0;
	else join(lc[x],rc[x]);
}

inline int pre(){
	int x=lc[rt];
	while(rc[x]) x=rc[x];
	splay(x);
	return val[x];
}

inline int nxt(){
	int x=rc[rt];
	while(lc[x]) x=lc[x];
	splay(x);
	return val[x];
}

int main(){
	n=gin();
	for(int i=1;i<=n;i++){
		int op=gin(),x=gin();
		switch(op){
			case 1:ins(x);break;
			case 2:del(x);break;
			case 3:printf("%d\n",rk(x));break;
			case 4:printf("%d\n",kth(x));break;
			case 5:ins(x);printf("%d\n",pre());del(x);break;
			case 6:ins(x);printf("%d\n",nxt());del(x);break;
		}
	}
	return 0;
}
```

upd 2021.6.10:[P6136 【模板】普通平衡树（数据加强版）](https://www.luogu.com.cn/problem/P6136)
```cpp
#include <bits/stdc++.h>
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

const int N=2e6+5;
int n,m,fa[N],lc[N],rc[N],val[N],sz[N],rt,tot,cnt[N];

inline void push(int x){
    if(x){
        sz[x]=cnt[x];
        if(lc[x]) sz[x]+=sz[lc[x]];
        if(rc[x]) sz[x]+=sz[rc[x]];
    }
    return;
}

void rotate(int x){
    int p=fa[x],g=fa[p];
    int b=lc[p]==x?rc[x]:lc[x];
    fa[x]=g,fa[p]=x;
    if(b) fa[b]=p;
    if(g) (lc[g]==p?lc[g]:rc[g])=x;
    if(x==lc[p]) rc[x]=p,lc[p]=b;
    else lc[x]=p,rc[p]=b;
    push(p);push(x);
}

inline bool wrt(int x){return x==rc[fa[x]];}
void splay(int x,int tar=0){
    while(fa[x]!=tar){
        if(fa[fa[x]]!=tar)
            wrt(x)==wrt(fa[x])?rotate(fa[x]):rotate(x);
        rotate(x);
    }
    if(!tar) rt=x;
}

inline int find(int v){
    int x=rt;
    while(x){
        if(v==val[x]) break;
        if(val[x]>v) x=lc[x];
        else x=rc[x];
    }
    if(x) splay(x);
    return x;
}

inline void ins(int v){
    int x=rt,p=0,dir=0;
    while(x){
        ++sz[p=x];
        if(v==val[x]){cnt[x]++;push(x);splay(x);return;}
        if(v< val[x]) x=lc[x],dir=0;
        else x=rc[x],dir=1;
    }
    x=++tot;
    fa[x]=p,val[x]=v,sz[x]=1,cnt[x]=1;
    if(p) (dir==0?lc[p]:rc[p])=x;
    push(p);
    splay(x);
}

inline void join(int u,int v){
    fa[u]=0,fa[v]=0;
    int w=u;
    while(rc[w]) w=rc[w];
    splay(w);
    rc[w]=v,fa[v]=w;
}

inline void del(int v){
    int x=find(v);
    if(cnt[x]>=2){cnt[x]--;push(x);return;}
    if(!lc[x] || !rc[x])
        fa[rt=lc[x]|rc[x]]=0;
    else join(lc[x],rc[x]);
}

inline int rk(int v){
    int x=find(v);
    return sz[lc[x]]+1;
}

inline int kth(int k){
    int x=rt,y=k;
    while(x){
        if(y<=sz[lc[x]]) x=lc[x];
        else {
            y-=sz[lc[x]]+cnt[x];
            if(y<=0){
                splay(x);
                return val[x];
            }
            x=rc[x];
        }
    }
}

inline int pre(){
    int x=lc[rt];
    while(rc[x]) x=rc[x];
    splay(x);
    return x;
}
inline int nxt(){
    int x=rc[rt];
    while(lc[x]) x=lc[x];
    splay(x);
    return x;
}

signed main(){
    n=gin(),m=gin();
    for(int i=1;i<=n;i++) ins(gin());
    int last=0,ans=0;
    for(int i=1;i<=m;i++){
        int op=gin(),x=gin();
        x^=last;
        switch(op){
            case 1:ins(x);break;
            case 2:del(x);break;
            case 3:ins(x);last=rk(x);del(x);break;
            case 4:last=kth(x);break;
            case 5:ins(x);last=val[pre()];del(x);break;
            case 6:ins(x);last=val[nxt()];del(x);break;
        }
        if(op>=3) ans^=last;
    }
    printf("%d\n",ans);
    return 0;
}
```
