---
title: 「复习」字符串算法
date: 2021-11-18 16:11:25
tag: 复习
category: 学习笔记
---

### KMP

```cpp
void pre() {
	fail[1]=0;
	for(int i=2,j=0;i<=m;i++) {
		while(j && s2[i]!=s2[j+1]) j=fail[j];
		if(s2[i]==s2[j+1]) j++;
		fail[i]=j;
	}
}

void kmp() {
	for(int i=1,j=0;i<=n;i++) {
		while(j && s1[i]!=s2[j+1]) j=fail[j];
		if(s1[i]==s2[j+1]) j++;
		if(j==m) printf("%d\n",i-m+1),j=fail[j];
	}
}
```

### Manacher

```cpp
void solve(char* a,int n) {
	for(int i=0,p=0,r=0;i<n;i++) {
		if(i<r) f[i]=min(f[2*p-i],r-i+1);
		else f[i]=1;
		while(0<=i-f[i] && i+f[i]<n && a[i-f[i]]==a[i+f[i]]) f[i]++;
		if(i+f[i]-1>r) p=i,r=i+f[i]-1;
	}
	for(int i=0;i<n;i++) f[i]--;
}
```

### Z函数

```cpp
vector<int> z_function(char* s) {
	int len=n+m+1;
	vector<int> z(len);
	for(int i=1,l=0,r=0;i<len;i++) {
		if(i<=r) z[i]=min(r-i+1,z[i-l]);
		while(i-z[i]<len && s[i+z[i]]==s[z[i]]) z[i]++;
		if(i+z[i]-1>r) l=i,r=i+z[i]-1;
	}
	z[0]=m;
	return z;
}
```