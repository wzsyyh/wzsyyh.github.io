---
title: 「复习」连通性相关
date: 2021-11-18 08:35:28
tag: 复习
category: 学习笔记
---

## 无向图连通性

### 割点、桥

记得最初接触这两个概念的时候是通过《一本通·提高篇》，那一章节的名称叫“割点和桥”，导致我一直以为这四个字合起来是一个名词，而其中的“和”其实仅仅是一个连词。

这两个概念简单来说就是：

> **割点：**从连通图中删去一个点 $x$ 以及所有 $x$ 连出去的边，删去后原图不再连通（即分裂成两个及以上个不相连的子图）。这样的点 $x$ 就是**割点**。
>
> **桥：**又称作**割边**。从连通图中删去一条边 $e$ 之后，原图分裂成了两个及以上个不相连的子图。这样的边 $e$ 就是**桥**。

#### 先来看**桥**：

删去 $(u,v)$ 之间的边后如果图不再连通了，思索一下发现 $v$ 的追溯值肯定是大于 $u$ 的。因为如果 $v$ 能追溯到时间戳小于/等于 $u$ 的话，不用通过这条边还能回到 $u$ 之上。

$$(u,v)是桥 \iff dfn[u] < low[v] $$

```cpp
int tot=1;
bool bdg[N<<1];

void tarjan(int u,int e) {
	dfn[u]=low[u]=++dfc;
	for(int i=head[u];i;i=ne[i]) {
		if(!dfn[v]) {
			tarjan(v,i);
			low[u]=min(low[u],low[v]);
			if(dfn[u]<low[v]) bdg[i]=bdg[i^1]=1; //即桥的判定条件
		}
		else if(i!=(e^1)) low[u]=min(low[u],dfn[v]);
	}
}
```

#### 再来看**割点**：

看起来它比**桥**更特别的地方，是既删去了点，又删去了边。思索一下，对于 $u$ 的**某一个**儿子 $v$，如果有 $dfn[u] \leq low[v]$，$u$ 似乎就是**割点**了。

但如果 $u$ 是根的话，不难发现它的所有儿子肯定都是满足这条式子的。然而如果 $u$ 只有一个环（大概是这样？），那删去了 $u$ 整个图还是非常的连通。所以对于根节点的情况，需要有**至少两个**儿子 $v$ 满足 $dfn[u] \leq low[v]$。

```cpp
bool cut[N];

void tarjan(int u,int fa) {
	dfn[u]=low[u]=++dfc;
	int flg=0;
	for(int i=head[u];i;i=ne[i]) {
		int v=to[i];
		if(!dfn[v]) {
			tarjan(v,u);
			low[u]=min(low[u],low[v]);
			if(dfn[u]<=low[v]) cut[u]=(u!=rt || ++flg>1); //即割点判定条件
		}
		else if(v!=fa) low[u]=min(low[u],dfn[v]);
	}
}
```

在写上面这段代码的时候，回看了下《进阶指南》以及以前在洛谷上提交的代码，发现书上和以前代码里都没有传参数`fa`，并且在上方的`else`处都没有判定`v!=fa`直接`low[u]=min(low[u],dfn[v])`了。但思考了片刻后发现这样处理出来的`low`数组，甚至跟之前求**桥**的代码中求出来的`low`数组不一样了，因为这样求把父亲的`dfn`也更新到了自己的`low`。这样处理的话在**求割点**这样一个特殊问题下不会造成问题，但仔细想想好像跟定义有些违背？

再看了下OI-wiki以及ljc的割点代码，都是有考虑目标点是否等于父亲的情况。最终感觉`if(v!=fa)`这个判定还是必要的。

正所谓*温故而知新*吧。

### 双连通分量

> **点双（v-DCC）：**不存在**割点**的图。
>
> **边双（e-DCC）：**不存在**桥**的图。

《进阶指南》上讲述的**定理**，大致是：

一张图是**点双**，当且仅当下列两个条件之一：

1. 顶点数不超过 $2$。
1. 图中任意两点都同时包含在至少一个简单环中。

一张图是**边双**，当且仅当任意一条边都包含在至少一个简单环中。

#### 边双的求法

把所有的**桥**都删掉，剩下来的连通块都是**边双**。

先标记出**桥**，然后再：

```cpp
void dfs(int u) {
	c[u]=dcc;
	for(int i=head[u];i;i=ne[i]) {
		int v=to[i];
		if(c[v] || bdg[i]) continue;
		dfs(v);
	}
}

signed main() {
	...

	for(int i=1;i<=n;i++) if(!c[i]) ++dcc,dfs(i);
	printf("There are %d e-DCCs.\n",dcc);
	for(int i=1;i<=n;i++)
		printf("%d belongs to DCC %d.\n",i,c[i]);

	...
	return 0;
}
```

#### 边双的缩点

只需先用上面的代码求出边双，再：

```cpp
signed main() {
	...

	for(int i=2;i<=tot;i++) {
		int u=to[i^1],v=to[i];
		if(c[u]!=c[v]) e[c[u]].push_back(c[v]); //懒得再写一个前向星了
	}
	//现在vector<int> e就是缩点后的图了，点数是 dcc ，边数可以再每次连边的时候++来统计。

	...
	return 0;
}
```

#### 点双的求法

> 一个容易跟定义混淆的事情：原图的割点可以在多个点双中。

求点双的方法就是在 **Tarjan** 的过程中维护一个栈，具体的：

```cpp
void tarjan(int u,int fa) {
	dfn[u]=low[u]=++dfc;
	st[++top]=u;
	if(u==rt && head[u]==0) {dcc[++cnt].push_back(u); return ;}
	int flg=0;
	for(int i=head[u];i;i=ne[i]) {
		int v=to[i];
		if(!dfn[v]) {
			tarjan(v,u);
			low[u]=min(low[u],low[v]);
			if(dfn[u]<=low[v]) {
				cut[u]=(u!=rt || ++flg>1);
				cnt++;
				int x;
				do {
					x=st[top--];
					dcc[cnt].push_back(x);
				} while(x!=v);
				dcc[cnt].push_back(u);
			}
		}
		else if(v!=fa) low[u]=min(low[u],dfn[v]);
	}
}

signed main() {
	...

	for(int i=1;i<=cnt;i++) {
		printf("v-DCC #%d:",i);
		for(int x:g[i]) printf(" %x");
		puts("");
	}// 这样就输出了每一个点双

	...
	return 0;
}
```

#### 点双的缩点

相比于边双的缩点，这个就比较阴间了。因为一个点双可能有好多个割点，一个割点又可能在好几个点双。

先用上面的方法求出点双和割点后：

```cpp
signed main() {
	...

	num=cnt;
	for(int i=1;i<=cnt;i++) if(cut[i]) new_id[i]=++num;
	for(int i=1;i<=cnt;i++)
		for(int x:dcc[i])
			if(cut[x]) V[i].push_back(new_id[x]),V[new_id[x]].push_back(i);
			//else c[x]=i; //如果要记录除了割点以外每个点属于的点双，加上这一句else即可
	//现在这个vector<int> V就是缩点后的图了

	...
	return 0;
}
```

#### 题！

*From: 某场模拟赛（jokers纪念日前一天的那场）*

*Problem:* 找出所有边，满足这些边恰好存在于一个简单环中。

*Solution:* 一个点双里肯定有环。当一个点双里边数大于点数时，每一条边都可以在两个不同的环中。所以题目要求等价于求**点数=边数**的点双中的边。

### 欧拉路问题

#### 欧拉回路（欧拉图）

条件：所有点度数都是偶数。

求法：

```cpp
int tot=1;

void dfs(int u) {
    for(int& i=head[u];i;i=ne[i]) {
        int v=to[i],j=i>>1;
        if(vis[j]) continue;
        vis[j]=1;
        int k=i;
        dfs(v);
        e[++el]=k;
    }
}
```

#### 欧拉路径

条件：只有两个点度数为奇数。这两个点也就是欧拉路径的两端。

代码只需在欧拉回路的基础上稍作修改。