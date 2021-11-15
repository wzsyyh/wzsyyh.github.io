---
title: 「学习笔记」扩展KMP
date: 2021-07-22 15:36:20
tag: [字符串]
category: [学习笔记]
---



## Template

```cpp
struct exkmp{

    int nxt[N],extend[N];

    void GetNext(){
        int a=0;
        nxt[0]=m;
        while(a<m-1 && t[a]==t[a+1]) a++;
        nxt[1]=a,a=1;
        for(int k=2;k<m;k++){
            int p=a+nxt[a]-1,L=nxt[k-a];
            if(k+L-1>=p){
                int j=(p-k+1)>0?p-k+1:0;
                while(k+j<m && t[k+j]==t[j]) j++;
                nxt[k]=j;
                a=k;
            }
            else nxt[k]=L;
        }
    }

    void GetExtend(){
        int a=0;
        while(a<m && s[a]==t[a]) a++;
        extend[0]=a,a=0;
        for(int k=1;k<n;k++){
            int p=a+extend[a]-1,L=nxt[k-a];
            if(k+L-1>=p){
                int j=(p-k+1)>0?(p-k+1):0;
                while(k+j<n && j<m && s[k+j]==t[j]) j++;
                extend[k]=j;
                a=k;
            }
            else extend[k]=L;
        }
    }

}K;
```