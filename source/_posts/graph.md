---
title: 「复习」简单图论
date: 2021-11-18 14:42:50
tag: 复习
category: 学习笔记
---

### 单元最短路

#### Dijkstra

```cpp
void dijkstra(int s) {
	memset(dis,0x3f,sizeof(dis));
	memset(vis,0,sizeof(vis));
	dis[s]=0;
	priority_queue<pi> q;
	q.push({0,s});
	while(!q.empty()) {
		int u=q.front(); q.pop();
		if(vis[u]) continue;
		vis[u]=1;
		for(int i=head[u];i;i=ne[i]) {
			int v=to[i];
			if(dis[v]>dis[u]+we[i]) {
				dis[v]=dis[u]+we[i];
				q.push({-dis[v],v});
			}
		}
	}
}
```

#### SPFA

```cpp
void spfa(int s) {
	memset(dis,0x3f,sizeof(dis));
	memset(vis,0,sizeof(vis));
	dis[s]=0,vis[s]=1;
	queue<int> q;
	q.push(s);
	while(!q.empty()) {
		int u=q.front(); q.pop();
		vis[u]=0;
		for(int i=head[u];i;i=ne[i]) {
			int v=to[i];
			if(dis[v]>dis[u]+we[i]) {
				dis[v]=dis[u]+we[i];
				if(!vis[v]) q.push(v);s
			}
 		}
	}
}
```

### 最小生成树

#### Kruskal

```cpp
int find(int x) {return x==fa[x]?x:fa[x]=find(fa[x]);}

void kruskal {
	for(int i=1;i<=m;i++) {
		int x=e[i].x,y=e[i].y;
		int fx=find(x),fy=find(y);
		if(fx==fy) continue;
		fa[x]=y; add(x,y),add(y,x);
	}
}
```

### 网络流

#### 最大流

```cpp
bool bfs() {
	for(int i=1;i<=n;i++) dis[i]=-1,cur[i]=head[i];
	dis[s]=0;
	queue<int> q;
	q.push(s);
	while(!q.empty()) {
		int u=q.front(); q.pop();
		for(int i=head[u];i;i=ne[i]) {
			int v=to[i];
			if(cap[i] && dis[v]==-1) dis[v]=dis[u]+1,q.push(v);
		}
	}
	return dis[t]!=-1;
}

int dfs(int u,int f) {
	if(u==t || f==0) return f;
	int flow=0,d;
	for(int& i=cur[u];i;i=ne[i]) {
		int v=to[i];
		if(dis[v]==dis[u]+1 && (d=dfs(v,min(f,cap[i])))) {
			flow+=d,f-=d,cap[i]-=d,cap[i^1]+=d;
			if(f==0) break;
		}
	}
	return flow;
}

ll maxflow(int s,int t) {
	ll flow=0;
	while(bfs()) flow+=dfs(s,inf);
	return flow;
}
```

#### 费用流

```cpp
bool spfa(int s,int t) {
	memset(dis,0x3f,sizeof(dis));
	memset(vis,0,sizeof(vis));
	dis[s]=0;
	queue<int> q;
	q.push(s);
	while(!q.empty()) {
		int u=q.front(); q.pop();
		for(int i=head[u];i;i=ne[i]) {
			int v=to[i];
			if(cap[i] && dis[v]>dis[u]+cost[i]) {
				dis[v]=dis[u]+cost[i];
				if(!vis[v]) q.push(v);
			}
		}
	}
	return dis[t]!=inf;
}

int dfs(int u,int f) {
	if(u==t || f==0) return f;
	vis[u]=1;
	int flow=0,d;
	for(int i=head[u];i;i=ne[i]) {
		int v=to[i];
		if(!vis[v] && dis[v]==dis[u]+cost[i] && (d=dfs(v,min(f,cap[i])))) {
			flow+=d,f-=d,cap[i]-=d,cap[i^1]+=d,res+=d*cost[i];
			if(f==0) break;
		}
	}
	vis[u]=0;
	return flow;
}

ll mcmf(int s,int t) {
	ll flow=0;
	while(spfa(s,t)) flow+=dfs(s,inf);
	return flow;
}
```