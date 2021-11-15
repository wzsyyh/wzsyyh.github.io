---
title: 「游记」WZOI Round#1
date: 2021-07-02 19:28:44
tag: 模拟赛
category: 赛后总结
---

2021-07-02 07:45~11:45

之前真的是比赛打太少了，做的很不顺。

### T1

Floyed带走100pts

### T2

想到了鸽巢原理，却没想到对前缀和用鸽巢原理。想到了就是sbt了。。。赛时爆搜50pts

### T3

开始题看错了结果写的有30pts，后来题看对了贪心0pts

想写这篇博客也就是因为T3吧。。。

这场模拟赛的AKer——ATue说：“求最小的最大，求最大的最小，当然是二分啊。”说的十分有理，但先前我脑海里却没有这样的思想，记得 [NOIP2018]赛道修建 那题也是如此。

想到是二分了，关键就在于怎么判断二分的这个点可行与否了

第一种：逆推。能到达a[x]的范围为[a[x]-mid,a[x]+mid] 。其实思维含量也挺高的QwQ

`28ms	2.24MB	C++	866B`

```cpp
#pragma GCC optimize("Ofast")
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

const int N=1e5+5;
int n;
int a[N];

bool check(int mid){
	if(abs(a[2]-a[1])>mid) return 0;
	int l=a[n]-mid,r=a[n]+mid;
	int x=n-1;
	while(x>2){
		if(l<=a[x] && a[x]<=r){
			l=a[x]-mid;
			r=a[x]+mid;
		}
		else {
			l=max(l,a[x]-mid);
			r=min(r,a[x]+mid);
		}
		x--;
	}
	if(l<=a[1] && a[1]<=r) return 1;
	if(l<=a[2] && a[2]<=r) return 1;
	return 0;
}

signed main(){
	n=gin()+2;
	for(int i=1;i<=n;i++)
		a[i]=gin();
	int l=1,r=1e9+1;
	while(l<r){
		int mid=l+r>>1;
		if(check(mid)) r=mid;
		else l=mid+1;
	}
	printf("%d\n",l);
	return 0;
}
```
ATue的st表判断，好强QwQ

`132ms	22.07MB	C++	1224B`

```cpp
#pragma GCC optimize("Ofast")
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

const int N=1e5+5;
int n,st[N],top,a[N],lg[N],mx[N][25],mn[N][25];

inline int getmx(int l,int r){
	int k=lg[r-l+1];
	return max(mx[l][k],mx[r-(1<<k)+1][k]);
}

inline int getmn(int l,int r){
	int k=lg[r-l+1];
	return min(mn[l][k],mn[r-(1<<k)+1][k]);
}

bool check(int mid){
	st[top=1]=1,st[++top]=2;
	for(int i=3;i<=n;i++){
		int j=st[top];
		while(top){
			if(a[j]-getmn(j,i)<=mid && getmx(j,i)-a[j]<=mid) break;
			else j=st[--top];			
		}
		if(!top) return 0;
		st[++top]=i;
	}
	return 1;
}

signed main(){
	n=gin()+2;
	lg[0]=-1;
	for(int i=1;i<=n;i++)
		mx[i][0]=mn[i][0]=a[i]=gin(),lg[i]=lg[i>>1]+1;
	for(int j=1;(1<<j)<n;j++) for(int i=1;i+(1<<j)-1<=n;i++)
		mx[i][j]=max(mx[i][j-1],mx[i+(1<<j-1)][j-1]),mn[i][j]=min(mn[i][j-1],mn[i+(1<<j-1)][j-1]);
	int l=abs(a[2]-a[1]),r=1e9+1;
	while(l<r){
		int mid=l+r>>1;
		if(check(mid)) r=mid;
		else l=mid+1;
	}
	printf("%d\n",l);
	return 0;
}

```

### T4

6^n加剪枝加Ofast能过诶

```cpp
#pragma GCC optimize("Ofast")
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

const int N=1<<14;
int cnt[N],f[N],ans[N],p[N],k,n;

inline bool cmp(int x,int y){
	return cnt[x]<cnt[y];
}
void init(){
	for(int i=0;i<k;i++)
		cnt[i]=cnt[i>>1]+(i&1),p[i]=i,ans[i]=-1;
	sort(p,p+k,cmp);
	return;
}

signed main(){
	n=gin();
	k=1<<n;
	init();
	for(int i=0;i<k;i++)
		scanf("%1d",f+i);
	for(int i=0;i<k;i++){
		for(int u=0;u<k;u++){
			if(~ans[u]) continue;
			int s=(k-1)^p[i];
			if(f[u]!=f[u&p[i]]) continue;
			bool flag=1;
			for(int v=s;v;v=(v-1)&s)
				if(f[u]!=f[u&p[i]|v]){
					flag=0;
					break;
				}
			if(flag) ans[u]=cnt[p[i]];
		}
	}
	for(int i=0;i<k;i++)
		printf("%d ",ans[i]);
	return 0;
}
```
