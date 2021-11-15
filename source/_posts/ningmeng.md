---
title: 「题解」[JSOI2011] 柠檬
date: 2021-05-29 19:48:45
tag: [题解, 动态规划]
category: 题解
---
体会这题决策单调性优化和斜率优化的写法上的不同

## 决策单调性优化
用了[这篇题解](https://www.luogu.com.cn/blog/pks-LOVING/solution-p5504)的思路
二分find时找出的断点满足，对于s[i]大于断点的i有决策x优于决策y
所以s[i]大于断点时就pop栈顶
单次 $O(logn)$ 查询断点，总复杂度 $O(nlogn)$
```cpp
//#pragma GCC optimize("Ofast")
#include <bits/stdc++.h>
#define int long long
#define o(a,b) st[a][b]
#define sz(k) st[k].size()
#define p(k) st[k].size()-1
#define q(k) st[k].size()-2
using namespace std;

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

const int N=1e5+5;
int n,f[N],a[N],b[10005],s[N];
vector<int> st[10005];

inline int calc(int x,int sum){
	return f[x-1]+a[x]*sum*sum;
}

inline int find(int x,int y){
	int ret=n+1;
	int l=1,r=n;
	while(l<=r){
		int mid=l+r>>1;
		if(calc(x,mid-s[x]+1)>=calc(y,mid-s[y]+1))
			ret=mid,r=mid-1;
		else l=mid+1;
	}
	return ret;
}

signed main(){
	n=gin();
	for(int i=1;i<=n;i++){
		a[i]=gin();
		s[i]=++b[a[i]];
	}
	for(int i=1;i<=n;i++){
		int c=a[i];
		while(sz(c)>=2 && find(o(c,q(c)),o(c,p(c)))<=find(o(c,p(c)),i))
			st[c].pop_back();
		st[c].push_back(i);
		while(sz(c)>=2 && find(o(c,q(c)),o(c,p(c)))<=s[i])
			st[c].pop_back();
		f[i]=calc(o(c,p(c)),s[i]-s[o(c,p(c))]+1);
	}
	printf("%lld\n",f[n]);
	return 0;
}
```

## 斜率优化
用了[这篇题解](https://newbielyx.blog.luogu.org/solution-p5504)的思路
展开转移式后，含j且不含i的项放左边，其余放右边，得到一个斜率式
也是通过这一题的这一写法，我才体会了斜率优化什么时候维护上凸壳、什么时候维护下凸壳
每个决策点入栈一次且最多出栈一次，故总复杂度 $O(n)$
```cpp
//#pragma GCC optimize("Ofast")
#include <bits/stdc++.h>
#define int long long
#define o(a,b) st[a][b]
#define sz(k) st[k].size()
#define p(k) st[k].size()-1
#define q(k) st[k].size()-2
using namespace std;

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

const int N=1e5+5;
int n,f[N],a[N],b[10005],s[N];
vector<int> st[10005];

inline int calc(int i,int j){
	return f[j-1]+a[i]*(s[i]-s[j]+1)*(s[i]-s[j]+1);
}

inline int X(int i){
	return s[i];
}
inline int Y(int i){
	return f[i-1]+a[i]*s[i]*s[i]-2*a[i]*s[i];
}
inline double slope(int i,int j){
	return 1.0*(Y(i)-Y(j))/(X(i)-X(j));
}

signed main(){
	n=gin();
	for(int i=1;i<=n;i++){
		a[i]=gin();
		s[i]=++b[a[i]];
	}
	for(int i=1;i<=n;i++){
		int c=a[i];
		while(sz(c)>=2 && slope(o(c,q(c)),o(c,p(c)))<=slope(o(c,p(c)),i))
			st[c].pop_back();
		st[c].push_back(i);
		while(sz(c)>=2 && calc(i,o(c,q(c)))>=calc(i,o(c,p(c))))
			st[c].pop_back();
		f[i]=calc(i,o(c,p(c)));
	}
	printf("%lld\n",f[n]);
	return 0;
}
```

## 两种写法的比较
从时间上看一个 $log$ 的差距还是很明显的
![](file://C:/Users/wzsyy/Documents/Gridea/post-images/1622292087102.png)