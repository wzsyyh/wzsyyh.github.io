---
title: 「学习笔记」AC自动机
date: 2021-04-01 22:20:46
tag: 字符串
category: 学习笔记
---
> 还记得2019年暑假，gy在英乐华翻开ybt提高篇的目录

## 概述

通常来讲，**KMP** 算法用来处理单模式串匹配问题。而若要处理多模式串的问题，就要引出 **AC自动机** 。

**AC自动机** 是以 **Trie** 的结构为基础，结合 **KMP** 的思想建立的。

## 步骤

1. 将所有模式串构建成一棵 **Trie** 树

1. 对 **Trie** 上所有节点构造失配指针（最长后缀）

1. 利用失配指针对主串进行匹配。

## 流程

- ### 构建指针

	记 $tr[p][c]=v$ 表示结点 $v$ 的父结点 $p$ 通过字符 $c$ 指向 $v$ 。
    
	记 $fail[u]$ 表示 $u$ 的失配指针，即 $u$ 的最长后缀。
   
	1. 若 $tr[u][i]$ 存在，则 $fail[tr[u][i]]$ 可以由 $fail[u]$ 增加一个字符 $i$ 得到
   
	1. 否则，直接将 $tr[u][i]$ 指向 $tr[fail[u]][i]$ 的状态 
    
	```cpp
	void build(){
		for(int i=0;i<26;i++)
			if(tr[0][i])q.push(tr[0][i]);
		while(q.size()){
			int u=q.front();
			q.pop();
			for(int i=0;i<26;i++){
				if(tr[u][i]){
					fail[tr[u][i]]=tr[fail[u]][i];
					q.push(tr[u][i]);
				}
				else tr[u][i]=tr[fail[u]][i];
			}
		}
	}
	```
- ### 匹配函数

	以[P3808 【模板】AC自动机（简单版）](https://www.luogu.com.cn/problem/P3808)的要求为例

	```cpp
	int query(char *s) {
		int u=0,res=0;
		for(int i=1;s[i];i++) {
			u=tr[u][t[i]-'a'];
			for(int j=u;j && e[j]!=-1;j=fail[j]){
				res+=e[j],e[j]=-1;
			}
		}
		return res;
	}
	```

## 板子

[P5357 【模板】AC自动机（二次加强版）](https://www.luogu.com.cn/problem/P5357)

```cpp
#include <bits/stdc++.h>
using namespace std;

const int N=2e5+5;
int head[N],to[N],ne[N],tot;
int n,tr[N][26],fail[N],ch,book[N],sz[N];
char s[N*10];
queue<int> q;

void build(){
	for(int i=0;i<26;i++)
		if(tr[0][i])q.push(tr[0][i]);
	while(q.size()){
		int u=q.front();
		q.pop();
		for(int i=0;i<26;i++){
			if(tr[u][i]){
				fail[tr[u][i]]=tr[fail[u]][i];
				q.push(tr[u][i]);
			}
			else tr[u][i]=tr[fail[u]][i];
		}
	}
}

inline void add(int u,int v){
	to[++tot]=v;
	ne[tot]=head[u];
	head[u]=tot;
}

void dfs(int u){
	for(int i=head[u];i;i=ne[i]){
		int v=to[i];
		dfs(v);
		sz[u]+=sz[v];
	}
}

int main(){
	scanf("%d",&n);
	for(int i=1;i<=n;i++){
		scanf("%s",s+1);
		int u=0;
		for(int j=1;s[j];j++){
			if(!tr[u][s[j]-'a'])tr[u][s[j]-'a']=++ch;
			u=tr[u][s[j]-'a'];
		}
		book[i]=u;
	}
	build();
	scanf("%s",s+1);
	for(int u=0,i=1;s[i];i++){
		u=tr[u][s[i]-'a'];
		sz[u]++;
	}
	for(int i=1;i<=ch;i++){
		add(fail[i],i);
	}
	dfs(0);
	for(int i=1;i<=n;i++)printf("%d\n",sz[book[i]]);
	return 0;
}

```
