---
title: 板子集合——备战ACM
date: 2024-10-21 20:30:00
tag: 学习笔记
category: 学习笔记
---

### 快速幂

```cpp
int qpow(int a,int b,int mod){
	int res=1;
	while(b){
		if(b&1) res=res*a%mod;
		a=a*a%mod;
		b>>=1;
	}
	return res%mod;
}
```

### ST表

```cpp
int n,m,st[N][25],lg[N];

lg[0]=-1;
for(int i=1;i<=n;i++) st[i][0]=gin(),lg[i]=lg[i>>1]+1;
for(int j=1;j<=lg[n];j++) for(int i=1;i+(1<<j)-1<=n;i++)
    st[i][j]=max(st[i][j-1],st[i+(1<<j-1)][j-1]);
while(m--) {
    int l=gin(),r=gin();
    int k=lg[r-l+1];
    printf("%d\n",max(st[l][k],st[r-(1<<k)+1][k]));
}
```

### 树状数组

```cpp
inline void add(int x,int k) {
    while(x<=n) {
        c[x]+=k;
        x+=x&-x;
    }
}

inline int sum(int x) {
    int res=0;
    while(x) {
        res+=c[x];
        x-=x&-x;
    }
    return res;
}
```

### 线段树

```cpp
void upd(int x,int l,int r,int pos,int d){
    if(l==r){
        sz[x]+=d;
        return ;
    }
    int mid=l+r>>1;
    if(pos<=mid) upd(ls,l,mid,pos,d);
    else upd(rs,mid+1,r,pos,d);
    pushup(x);
}

void clear(int x,int l,int r,int L,int R){
    if(l==r){
        sz[x]=0;
        return ;
    }
    int mid=l+r>>1;
    if(L<=mid) clear(ls,l,mid,L,R);
    if(R> mid) clear(rs,mid+1,r,L,R);
    pushup(x);
}

int ask(int x,int l,int r,int L,int R){
    if(l>R || r<L) return 0;
    if(L<=l&&r<=R) return sz[x];
    int mid=l+r>>1;
    return ask(ls,l,mid,L,R)+ask(rs,mid+1,r,L,R);
}

int kth(int x,int l,int r,int k){
    if(l==r) return l;
    int mid=l+r>>1,t=sz[rs];
    if(k<=t) return kth(rs,mid+1,r,k);
    else return kth(ls,l,mid,k-t);
}
```