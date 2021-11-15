---
title: 「学习笔记」左偏树
date: 2021-04-22 08:46:11
tag: 数据结构
category: 学习笔记
---
```cpp
//合并 
int merge(int x,int y){
	if(!x || !y) return x|y;
	if(t[x].key>t[y].key) swap(x,y);
	t[t[x].rs=merge(t[x].rs,y)].fa=x;
	if(t[t[x].rs].d>t[t[x].ls].d) swap(t[x].ls,t[x].rs);
	t[x].d=t[t[x].rs].d+1;
	return x;
}
//构建
void build(){
	int l=1,r=n;
	for(int i=1;i<n;i++){//可证只有n-1次合并
		h[++r]=merge(h[l],h[l+1]);
		l+=2;
	}
}
//删除任意结点(pop)
void pushup(int x){
	if(!x) return;
	if(t[x].d!=t[t[x].rs].d+1){
		t[x].d=t[t[x].rs].d+1;
		pushup(t[x].fa);
	}
}

int merge(int x,int y){
	if(!x || !y) return x|y;
	if(t[x].key>t[y].key) swap(x,y);
	t[t[x].rs=merge(t[x].rs,y)].fa=x;
	if(t[t[x].rs].d>t[t[x].ls].d) swap(t[x].ls,t[x].rs);
	pushup(x);
	return x;
}

int pop(int x){
	return merge(t[x].ls,t[x].rs);
}
//整个堆加/减去一个值、乘上一个正数，在根上打标记，下传
int merge(int x,int y){
	if(!x || !y) return x|y;
	if(t[x].key>t[y].key) swap(x,y);
	pushdown(x);
	t[t[x].rs=merge(t[x].rs,y)].fa=x;
	if(t[t[x].rs].d>t[t[x].ls].d) swap(t[x].ls,t[x].rs);
	pushup(x);
	return x;
}

int pop(int x){
	pushdown(x);
	return merge(t[x].ls,t[x].rs);
}
//随机合并
int merge(int x,int y){
	if(!x || !y) return x|y;
	if(t[x].key>t[y].key) swap(x,y);
	if(rand()&1) swap(t[x].ls,t[x].rs);
	t[x].ls=merge(t[x].ls,y);
	return x;
}
//最终的板子
void pushup(int x){
	if(!x) return;
	if(t[x].d!=t[t[x].rs].d+1){
		t[x].d=t[t[x].rs].d+1;
		pushup(t[x].fa);
	}
}

int merge(int x,int y){
	if(!x || !y) return x|y;
	if(t[x].key>t[y].key) swap(x,y);
	pushdown(x);
	t[t[x].rs=merge(t[x].rs,y)].fa=x;
	if(t[t[x].rs].d>t[t[x].ls].d) swap(t[x].ls,t[x].rs);
	pushup(x);
	return x;
}

int pop(int x){
	pushdown(x);
	return merge(t[x].ls,t[x].rs);
}
```
