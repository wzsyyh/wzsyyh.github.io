---
title: 「题解」[APIO2019]路灯
date: 2021-05-17 21:26:41
tag: [题解, 数据结构, 技巧]
category: 题解
---
## 思路
对于一段连续的能够互相到达的站点，这里不妨称它为一个**连通块**
考虑用线段树维护每一个连通块
对于一个连通块里的每一个站点，存下这个连通块的左右端点（即一个站点所能到达的最左端和最右端）
对于一次连通块改变的操作，以操作的时刻 $t$ 来记录对答案产生的贡献
- 若为插入操作，对修改的区间贡献为 $-t$
- 若为删除操作，对修改的区间贡献为 $t$

**特别的**：询问时刻如果两点是连通的，记录答案 $+t$
这样处理可以很方便的解决某两点连通的时长
考虑切换第 $k$ 个路灯的状态对 $k$ 与 $k+1$ 所在连通块的影响
- 第 $k$ 个路灯原先是亮的
    - 相当于把这个连通块以 $k$ 与 $k+1$ 之间为断点分成 2 个连通块
    - 具体的，在线段树中查询得到左右端点 $l$ 和 $r$，修改 $[l,k]$ 和 $[k+1,r]$ 分别为 1 个连通块
- 第 $k$ 个路灯原先是灭的
    - 相当于是将 $k$ 和 $k+1$ 所在的 2 个连通块合并成 1 个
    - 具体的，查询 $k$ 所能到达的左端点和 $k+1$ 所能到达的右端点，记为 $l$ 和 $r$，修改 $[l,r]$ 为 1 个连通块

每次操作的贡献的区间修改，可以转化为二维平面上的矩形加，于是可以用容斥的思想在矩形上差分
比如对于 $[l,k]$ 和 $[k+1,r]$ 这两个区间的一次插入操作，看做是插入 $[l,k+1]、[k,r]$ 并删除 $[l,r]、[k,k+1]$
二维的矩形加上时间这一维 => 三维数点问题
这里我用 **CDQ分治** 实现
~~由于码力太弱~~，在题解和 [阿丑](https://www.luogu.com.cn/user/364963) 神佬的帮助下完成
## CODE
```cpp
//#pragma GCC optimize("Ofast") 
#include <bits/stdc++.h>
#define int long long
#define ls x<<1
#define rs x<<1|1
using namespace std;
typedef pair<int,int> pi;

inline int gin(){
	char c=getchar();
	int s=0,f=1;
	while(c<'0' || c>'9'){
		if(c=='-')f=-1;
		c=getchar();
	}
	while(c>='0'&&c<='9'){
		s=(s<<3)+(s<<1)+(c^48);
		c=getchar();
	}
	return s*f;
}

const int N=6e5+5;
char s[N];
int n,Q,tot,c[N],a[N],ans[N];
bool vis[N];

struct seg{
	pi py;
	bool tag;
} tr[N<<2];

struct node{
	int op,x,y1,y2,id,v;
} t[N],tmp[N];

void pushdown(int x){
	if(tr[x].tag){
		tr[ls].py=tr[rs].py=tr[x].py;
		tr[ls].tag=tr[rs].tag=1;
		tr[x].tag=0;
	}
}

void build(int x,int l,int r){
	if(l==r){
		tr[x].py=make_pair(l,l);
		return;
	}
	int mid=l+r>>1;
	build(ls,l,mid);
	build(rs,mid+1,r);
}

void change(int x,int l,int r,int L,int R,pi d){
	if(L<=l && r<=R){
		tr[x].py=d;
		tr[x].tag=1;
		return;
	}
	pushdown(x);
	int mid=l+r>>1;
	if(L<=mid) change(ls,l,mid,L,R,d);
	if(mid< R) change(rs,mid+1,r,L,R,d);
}

pi query(int x,int l,int r,int p){
	if(l==r) return tr[x].py;
	pushdown(x);
	int mid=l+r>>1;
	if(p<=mid) return query(ls,l,mid,p);
	else return query(rs,mid+1,r,p);
}

void upd(int x,int d){
	while(x<=n+1){
		c[x]+=d;
		x+=x&-x;
	}
}
void del(int x){
	while(x<=n+1){
		if(c[x]) c[x]=0;
		else break;
		x+=x&-x;
	}
}
int ask(int x){
	int res=0;
	while(x){
		res+=c[x];
		x-=x&-x;
	}
	return res;
}

void cdq(int l,int r) {
	if(l==r) return;
	int mid=l+r>>1,p=l,q=mid+1;
	cdq(l,mid),cdq(mid+1,r);
	for(int i=l;i<=r;i++){
		if(q>r || p<=mid && t[p].x<=t[q].x){
			tmp[i]=t[p++];
			if(tmp[i].op==2) continue;
			upd(tmp[i].y1,tmp[i].v);
			upd(tmp[i].y2+1,-tmp[i].v);
		}
		else {
			tmp[i]=t[q++];
			if(tmp[i].op==2) ans[tmp[i].id]+=ask(tmp[i].y1);
		}
	}
	for(int i=l;i<=r;i++){
		t[i]=tmp[i];
		if(t[i].op==1){
			del(tmp[i].y1);
			del(tmp[i].y2+1);
		}
	}
	return;
}

signed main(){
	n=gin(),Q=gin();
	scanf("%s",s);
	for(int i=1;i<=n;i++)
		a[i]=s[i-1]-'0';
	build(1,1,n+1);
	for(int i=1;i<=n;i++)
		if(a[i]==1 && !vis[i]){
			int j=i;
			vis[i]=1;
			while(a[j]) vis[++j]=1;
			change(1,1,n+1,i,j,make_pair(i,j));
		}
	memset(vis,0,sizeof(vis));
	int tot=0;
	for(int i=1;i<=Q;i++){
		scanf("%s",s);
		t[++tot].op=(s[0]=='t' ? 1 : 2);
		t[tot].id=i;
		if(t[tot].op==1){
			int k=gin();
			++tot, t[tot]=t[tot-1];
			if(a[k]==1){
				pi u=query(1,1,n+1,k);
				t[tot-1].x=u.first,t[tot].x=k+1;
				t[tot-1].y1=t[tot].y1=k+1,t[tot-1].y2=t[tot].y2=u.second;
				t[tot-1].v=i, t[tot].v=-i;
				change(1,1,n+1,u.first,k,make_pair(u.first,k));
				change(1,1,n+1,k+1,u.second,make_pair(k+1,u.second));
			}
			else {
				pi p1=query(1,1,n+1,k),p2=query(1,1,n+1,k+1);
				t[tot-1].x=p1.first,t[tot].x=k+1;
				t[tot-1].y1=t[tot].y1=k+1,t[tot-1].y2=t[tot].y2=p2.second;
				t[tot-1].v=-i, t[tot].v=i;
				change(1,1,n+1,p1.first,p2.second,make_pair(p1.first,p2.second));
			}
			a[k]^=1;
		}
		else {
			t[tot].x=gin(),t[tot].y1=gin();
			pi p=query(1,1,n+1,t[tot].x);
			if(p.second>=t[tot].y1)
				ans[i]+=i;
			vis[i]=1;
		}
	}
	cdq(1,tot);
	for(int i=1;i<=Q;i++)
		if(vis[i])
			printf("%lld\n",ans[i]);
	return 0;
}
```