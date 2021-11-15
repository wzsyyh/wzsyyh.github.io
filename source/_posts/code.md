---
title: CODE
date: 2021-10-19 18:37:16
tag: 
category: 
---

### CF504E

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef pair<int,int> pi;
typedef long long ll;
inline int gin() {
    int s=0,f=1;
    char c=getchar();
    while(c<'0' || c>'9') {
        if(c=='-') f=-1;
        c=getchar();
    }
    while(c>='0'&&c<='9') {
        s=(s<<3)+(s<<1)+(c^48);
        c=getchar();
    }
    return s*f;
}

const int N=3e5+5,mod=1e9+7;
int n,m,dep[N],sz[N],son[N],fa[N],dfn[N],zmz[N],top[N],dfc;
char str[N];
const pi B={131,13331};
pi bin[N],h1[N],h2[N];
vector<int> e[N];

inline pi operator + (pi a,pi b) {return {(a.first+b.first)%mod,(a.second+b.second)%mod};}
inline pi operator - (pi a,pi b) {return {(a.first-b.first+mod)%mod,(a.second-b.second+mod)%mod};}
inline pi operator * (pi a,pi b) {return {1ll*a.first*b.first%mod,1ll*a.second*b.second%mod};}
inline pi Hash(bool op,int x,int k) {
    if(op) return h2[x-k+1]-h2[x+1]*bin[k];
    return h1[x+k-1]-h1[x-1]*bin[k];
}

void dfs1(int u,int f) {
    sz[u]=1,dep[u]=dep[fa[u]=f]+1;
    for(int v:e[u]) if(v!=f) {
        dfs1(v,u);
        sz[u]+=sz[v];
        if(sz[v]>sz[son[u]]) son[u]=v;
    }
}

void dfs2(int u,int topf) {
    top[u]=topf,dfn[u]=++dfc,zmz[dfc]=u;
    if(son[u]) dfs2(son[u],topf);
    for(int v:e[u]) if(!top[v]) dfs2(v,v);
}

int lca(int x,int y) {
    while(top[x]!=top[y]) {
        if(dep[top[x]]<dep[top[y]]) swap(x,y);
        x=fa[top[x]];
    }
    return dep[x]<dep[y]?x:y;
}

vector<pi> get(int x,int y) {
    int z=lca(x,y);
    // puts("Yes?");
    vector<pi> q1,q2;
    while(dep[top[x]]>dep[z]) q1.push_back({x,top[x]}),x=fa[top[x]];
    // puts("Why?");
    q1.push_back({x,z});
    while(dep[top[y]]>dep[z]) q2.push_back({top[y],y}),y=fa[top[y]];
    // puts("Sure?");
    if(y!=z) q2.push_back({son[z],y});
    while(q2.size()) q1.push_back(q2.back()),q2.pop_back();
    return q1;
}

signed main() {
    #ifndef ONLINE_JUDGE
    freopen("test.in","r",stdin);
    freopen("test.out","w",stdout);
    #endif
    n=gin();
    scanf("%s",str+1);
    bin[0]={1,1},bin[1]=B;
    for(int i=1;i<n;i++) {
        int u=gin(),v=gin();
        e[u].push_back(v),e[v].push_back(u);
        bin[i+1]=bin[i]*B;
    }
    dfs1(1,0);
    dfs2(1,1);
    for(int i=1;i<=n;i++) {
        h1[i]=h1[i-1]*B+(pi){str[zmz[i]],str[zmz[i]]};
        h2[n-i+1]=h2[n-i+2]*B+(pi){str[zmz[n-i+1]],str[zmz[n-i+1]]};
    }
    m=gin();
    while(m--) {
        int a=gin(),b=gin(),c=gin(),d=gin(),ans=0,s=0,t=0;
        vector<pi> f=get(a,b),g=get(c,d);
        // puts("#");
        while(s<f.size() && t<g.size()) {
            // puts("@");
            int fl=dfn[f[s].first],fr=dfn[f[s].second];
            int gl=dfn[g[t].first],gr=dfn[g[t].second];
            bool tf=fl>fr,tg=gl>gr;
            int lenf=(tf?fl-fr:fr-fl)+1;
            int leng=(tg?gl-gr:gr-gl)+1;
            int len=min(lenf,leng);
            pi hf=Hash(tf,fl,len);
            pi hg=Hash(tg,gl,len);
            if(hf==hg) {
                if(len==lenf) s++;
                else f[s].first=zmz[fl+(tf?-1:1)*len];
                if(len==leng) t++;
                else g[t].first=zmz[gl+(tg?-1:1)*len];
                ans+=len;
            }
            else {
                int l=1,r=len;
                while(l<r) {
                    int mid=l+r>>1;
                    hf=Hash(tf,fl,mid);
                    hg=Hash(tg,gl,mid);
                    if(hf==hg) l=mid+1;
                    else r=mid;
                }
                ans+=l-1;
                break;
            }
        }
        printf("%d\n",ans);
    }
    return 0;
}
```

### CF547D

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef pair<int,int> pi;
typedef long long ll;
inline int gin() {
    int s=0,f=1;
    char c=getchar();
    while(c<'0' || c>'9') {
        if(c=='-') f=-1;
        c=getchar();
    }
    while(c>='0'&&c<='9') {
        s=(s<<3)+(s<<1)+(c^48);
        c=getchar();
    }
    return s*f;
}

const int N=2e5+5;
int n,prex[N],prey[N],col[N];
vector<int> g[N];

void dfs(int u) {
    for(int v:g[u]) if(col[v]==-1) col[v]=!col[u],dfs(v);
}

signed main() {
    #ifndef ONLINE_JUDGE
    freopen("test.in","r",stdin);
    freopen("test.out","w",stdout);
    #endif
    n=gin();
    for(int i=1;i<=n;i++) {
        int x=gin(),y=gin();
        col[i]=-1;
        if(!prex[x]) prex[x]=i;
        else g[prex[x]].push_back(i),g[i].push_back(prex[x]),prex[x]=0;
        if(!prey[y]) prey[y]=i;
        else g[prey[y]].push_back(i),g[i].push_back(prey[y]),prey[y]=0;
    }
    for(int i=1;i<=n;i++) if(col[i]==-1) col[i]=0,dfs(i);
    for(int i=1;i<=n;i++) putchar(col[i]?'b':'r');
    return 0;
}
```

### CF527E

```cpp
#include <bits/stdc++.h>
#define int long long
using namespace std;
typedef pair<int,int> pi;
typedef long long ll;
inline int gin() {
    int s=0,f=1;
    char c=getchar();
    while(c<'0' || c>'9') {
        if(c=='-') f=-1;
        c=getchar();
    }
    while(c>='0'&&c<='9') {
        s=(s<<3)+(s<<1)+(c^48);
        c=getchar();
    }
    return s*f;
}

const int N=1e5+5,M=3e5+5;
int n,m,st[N],top,num,e[M<<1],el;
int tot=1,head[N],to[M<<1],ne[M<<1],fr[M<<1],ind[N];
bool tag[N],vis[M];

inline void add(int u,int v) {to[++tot]=v,fr[tot]=u,ind[v]++,ne[tot]=head[u],head[u]=tot;}

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

signed main() {
    #ifndef ONLINE_JUDGE
    freopen("test.in","r",stdin);
    freopen("test.out","w",stdout);
    #endif
    n=gin(),m=gin();
    for(int i=1;i<=m;i++) {
        int u=gin(),v=gin();
        add(u,v),add(v,u);
    }
    for(int i=1;i<=n;i++) if(ind[i]&1) st[++top]=i;
    for(int i=1;i<top;i+=2) add(st[i],st[i+1]),add(st[i+1],st[i]);
    int len=m+top/2;
    if(len&1) add(1,1),add(1,1),len++;
    dfs(1);
    printf("%lld\n",len);
    for(int i=1;i<=el;i++) {
        int j=e[i]^((++num)&1);
        printf("%lld %lld\n",fr[j],to[j]);
    }
    return 0;
}
```

### BZOJ2839

```cpp
#include <bits/stdc++.h>
using namespace std;
inline int gin() {
    int s=0,f=1;
    char c=getchar();
    while(c<'0' || c>'9') {
        if(c=='-') f=-1;
        c=getchar();
    }
    while(c>='0'&&c<='9') {
        s=(s<<3)+(s<<1)+(c&15);
        c=getchar();
    }
    return s*f;
}

const int N=1e6+5,mod=1e9+7;
int inv[N],fact[N],finv[N];

void init() {
    inv[1]=1;
    for(int i=2;i<=1e6;i++) inv[i]=1ll*(mod-mod/i)*inv[mod%i]%mod;
    fact[0]=finv[0]=1;
    for(int i=1;i<=1e6;i++) {
        fact[i]=1ll*fact[i-1]*i%mod;
        finv[i]=1ll*finv[i-1]*inv[i]%mod;
    }
}

int C(int n,int m) {
    if(m<0 || m>n) return 0;
    return 1ll*fact[n]*finv[m]%mod*finv[n-m]%mod;
}

int qpow(int a,int b,int mod) {
    int res=1;
    while(b) {
        if(b&1) res=1ll*res*a%mod;
        a=1ll*a*a%mod;
        b>>=1;
    }
    return res;
}

signed main() {
    init();
    int n=gin(),k=gin(),ans=0;
    for(int i=k;i<=n;i++) {
        ans=(ans+1ll*((i-k)%2?-1:1)*C(i,k)*C(n,i)%mod*(qpow(2,qpow(2,n-i,mod-1),mod))%mod)%mod;
    }
    printf("%d\n",(ans+mod)%mod);
    return 0;
}
```

### gym101933K

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef pair<int,int> pi;
typedef long long ll;
inline int gin() {
    int s=0,f=1;
    char c=getchar();
    while(c<'0' || c>'9') {
        if(c=='-') f=-1;
        c=getchar();
    }
    while(c>='0'&&c<='9') {
        s=(s<<3)+(s<<1)+(c^48);
        c=getchar();
    }
    return s*f;
}

const int N=2505,mod=1e9+7;
int n,k,inv[N],fact[N],finv[N],ans;

void init() {
    inv[1]=1;
    for(int i=2;i<=2500;i++) inv[i]=1ll*(mod-mod/i)*inv[mod%i]%mod;
    fact[0]=finv[0]=1;
    for(int i=1;i<=2500;i++) {
        fact[i]=1ll*fact[i-1]*i%mod;
        finv[i]=1ll*finv[i-1]*inv[i]%mod;
    }
}

int C(int n,int m) {
    if(m<0 || m>n) return 0;
    return 1ll*fact[n]*finv[m]%mod*finv[n-m]%mod;
}

int qpow(int a,int b) {
    int res=1;
    while(b) {
        if(b&1) res=1ll*res*a%mod;
        a=1ll*a*a%mod;
        b>>=1;
    }
    return res;
}

signed main() {
    #ifndef ONLINE_JUDGE
    freopen("test.in","r",stdin);
    freopen("test.out","w",stdout);
    #endif
    init();
    n=gin(),k=gin();
    for(int i=1;i<n;i++) gin();
    for(int i=1;i<=k;i++)
        ans=(ans+1ll*((i-k)%2?-1:1)*C(k,i)*i%mod*qpow(i-1,n-1)%mod+mod)%mod;
    printf("%d\n",ans);
    return 0;
}
```

### BZOJ4710

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef pair<int,int> pi;
typedef long long ll;
inline int gin() {
    int s=0,f=1;
    char c=getchar();
    while(c<'0' || c>'9') {
        if(c=='-') f=-1;
        c=getchar();
    }
    while(c>='0'&&c<='9') {
        s=(s<<3)+(s<<1)+(c^48);
        c=getchar();
    }
    return s*f;
}

const int N=2005,mod=1e9+7;
int a[N],f[N];
int inv[N],fact[N],finv[N];

void init() {
    inv[1]=1;
    for(int i=2;i<=2000;i++) inv[i]=1ll*(mod-mod/i)*inv[mod%i]%mod;
    fact[0]=finv[0]=1;
    for(int i=1;i<=2000;i++) {
        fact[i]=1ll*fact[i-1]*i%mod;
        finv[i]=1ll*finv[i-1]*inv[i]%mod;
    }
}

int C(int n,int m) {
    if(m<0 || m>n) return 0;
    return 1ll*fact[n]*finv[m]%mod*finv[n-m]%mod;
}

signed main() {
    #ifndef ONLINE_JUDGE
    freopen("test.in","r",stdin);
    freopen("test.out","w",stdout);
    #endif
    init();
    int n=gin(),m=gin();
    for(int i=1;i<=m;i++) a[i]=gin();
    for(int i=0;i<n;i++) {
        f[i]=C(n,i);
        // printf("%d ",f[i]);
        for(int j=1;j<=m;j++) f[i]=1ll*f[i]*C(a[j]+n-i-1,n-i-1)%mod;
        // printf("%d\n",f[i]);
    }
    int ans=0;
    for(int i=0;i<n;i++) ans=(ans+(i%2?-1:1)*f[i])%mod;
    printf("%d\n",(ans+mod)%mod);
    return 0;
}
```

### BZOJ4487

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef pair<int,int> pi;
typedef long long ll;
inline int gin() {
    int s=0,f=1;
    char c=getchar();
    while(c<'0' || c>'9') {
        if(c=='-') f=-1;
        c=getchar();
    }
    while(c>='0'&&c<='9') {
        s=(s<<3)+(s<<1)+(c^48);
        c=getchar();
    }
    return s*f;
}

const int N=405,mod=1e9+7;
int n,m,c,bin[N*N],ans;
int inv[N],fact[N],finv[N];

void init() {
    inv[1]=1;
    for(int i=2;i<=400;i++) inv[i]=1ll*(mod-mod/i)*inv[mod%i]%mod;
    fact[0]=finv[0]=1;
    for(int i=1;i<=400;i++) {
        fact[i]=1ll*fact[i-1]*i%mod;
        finv[i]=1ll*finv[i-1]*inv[i]%mod;
    }
}

int C(int n,int m) {
    if(m<0 || m>n) return 0;
    return 1ll*fact[n]*finv[m]%mod*finv[n-m]%mod;
}

signed main() {
    #ifndef ONLINE_JUDGE
    freopen("test.in","r",stdin);
    freopen("test.out","w",stdout);
    #endif
    init();
    n=gin(),m=gin(),c=gin();
    for(int k=0;k<=c;k++) {
        bin[0]=1;
        for(int i=1;i<=n*m;i++) bin[i]=1ll*bin[i-1]*(c-k+1)%mod;
        for(int i=0;i<=n;i++) for(int j=0;j<=m;j++)
            ans=(ans+1ll*((i+j+k)&1?(mod-1):1)*C(n,i)%mod*C(m,j)%mod*C(c,k)%mod*bin[(n-i)*(m-j)]%mod)%mod;
    }
    printf("%d\n",ans);
    return 0;
}
```

### CF1228E

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef pair<int,int> pi;
typedef long long ll;
inline int gin() {
    int s=0,f=1;
    char c=getchar();
    while(c<'0' || c>'9') {
        if(c=='-') f=-1;
        c=getchar();
    }
    while(c>='0'&&c<='9') {
        s=(s<<3)+(s<<1)+(c^48);
        c=getchar();
    }
    return s*f;
}

const int N=255,mod=1e9+7;
int n,k,bin[N*N],bin1[N*N],ans;
int inv[N],fact[N],finv[N];

void init() {
    inv[1]=1;
    for(int i=2;i<=250;i++) inv[i]=1ll*(mod-mod/i)*inv[mod%i]%mod;
    fact[0]=finv[0]=1;
    for(int i=1;i<=250;i++) {
        fact[i]=1ll*fact[i-1]*i%mod;
        finv[i]=1ll*finv[i-1]*inv[i]%mod;
    }
}

int C(int n,int m) {
    if(m<0 || m>n) return 0;
    return 1ll*fact[n]*finv[m]%mod*finv[n-m]%mod;
}

int qpow(int a,int b) {
    int res=1;
    while(b) {
        if(b&1) res=1ll*res*a%mod;
        a=1ll*a*a%mod;
        b>>=1;
    }
    return res;
}

signed main() {
    #ifndef ONLINE_JUDGE
    freopen("test.in","r",stdin);
    freopen("test.out","w",stdout);
    #endif
    init();
    n=gin(),k=gin();
    for(int i=0;i<=n;i++) for(int j=0;j<=n;j++)
        (ans+=1ll*((i+j)&1?(mod-1):1)*C(n,i)%mod*C(n,j)%mod*qpow(k,(n-i)*(n-j))%mod*qpow(k-1,n*n-(n-i)*(n-j))%mod)%=mod;
    printf("%d\n",ans);
    return 0;
}
```

### CF997C

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef pair<int,int> pi;
typedef long long ll;
inline int gin() {
    int s=0,f=1;
    char c=getchar();
    while(c<'0' || c>'9') {
        if(c=='-') f=-1;
        c=getchar();
    }
    while(c>='0'&&c<='9') {
        s=(s<<3)+(s<<1)+(c^48);
        c=getchar();
    }
    return s*f;
}

const int N=1e6+5,mod=998244353;
int n,ans;
int inv[N],fact[N],finv[N];

void init() {
    inv[1]=1;
    for(int i=2;i<=1e6;i++) inv[i]=1ll*(mod-mod/i)*inv[mod%i]%mod;
    fact[0]=finv[0]=1;
    for(int i=1;i<=1e6;i++) {
        fact[i]=1ll*fact[i-1]*i%mod;
        finv[i]=1ll*finv[i-1]*inv[i]%mod;
    }
}

int C(int n,int m) {
    if(m<0 || m>n) return 0;
    return 1ll*fact[n]*finv[m]%mod*finv[n-m]%mod;
}

int qpow(int a,int b) {
    int res=1;
    while(b) {
        if(b&1) res=1ll*res*a%mod;
        a=1ll*a*a%mod;
        b>>=1;
    }
    return res;
}

signed main() {
    #ifndef ONLINE_JUDGE
    freopen("test.in","r",stdin);
    freopen("test.out","w",stdout);
    #endif
    init();
    n=gin();
    for(int i=1;i<=n;i++)
        (ans+=1ll*((i&1)?(mod-1):1)*C(n,i)%mod*qpow(3,1ll*(mod-1-i)*n%(mod-1))%mod*(qpow((1-qpow(3,i-n+mod-1)+mod)%mod,n)-1+mod)%mod)%=mod;
    ans=1ll*ans*qpow(3,(1ll*n*n+1)%(mod-1))%mod;
    // printf("%d\n",(ans+mod)%mod);
    (ans+=2ll*qpow(3,1ll*n*n%(mod-1))%mod*(qpow(1-qpow(3,(1-n+mod-1)%(mod-1)),n)-1)%mod)%=mod;
    printf("%d\n",(mod-ans)%mod);
    return 0;
}
```

### BZOJ3622

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef pair<int,int> pi;
typedef long long ll;
inline int gin() {
    int s=0,f=1;
    char c=getchar();
    while(c<'0' || c>'9') {
        if(c=='-') f=-1;
        c=getchar();
    }
    while(c>='0'&&c<='9') {
        s=(s<<3)+(s<<1)+(c^48);
        c=getchar();
    }
    return s*f;
}

const int N=2005,mod=1e9+9;
int n,k,f[N][N],ans,a[N],b[N],F[N],L[N];
int inv[N],fact[N],finv[N];

void init() {
    inv[1]=1;
    for(int i=2;i<=2000;i++) inv[i]=1ll*(mod-mod/i)*inv[mod%i]%mod;
    fact[0]=finv[0]=1;
    for(int i=1;i<=2000;i++) {
        fact[i]=1ll*fact[i-1]*i%mod;
        finv[i]=1ll*finv[i-1]*inv[i]%mod;
    }
}

int C(int n,int m) {
    if(m<0 || m>n) return 0;
    return 1ll*fact[n]*finv[m]%mod*finv[n-m]%mod;
}

signed main() {
    #ifndef ONLINE_JUDGE
    freopen("test.in","r",stdin);
    freopen("test.out","w",stdout);
    #endif
    init();
    n=gin(),k=gin();
    if((n+k)&1) puts("0"),exit(0);
    k=n+k>>1;
    for(int i=1;i<=n;i++) a[i]=gin();
    for(int i=1;i<=n;i++) b[i]=gin();
    sort(a+1,a+n+1), sort(b+1,b+n+1);
    for(int i=1,j=0;i<=n;i++) {
        while(j<n && a[i]>b[j+1]) j++;
        L[i]=j;
    }
    f[0][0]=1;
    for(int i=1;i<=n;i++) for(int j=0;j<=i;j++)
        f[i][j]=(f[i-1][j]+(j?1ll*f[i-1][j-1]*(L[i]-j+1)%mod:0))%mod;
    for(int i=0;i<=n;i++) F[i]=1ll*f[n][i]*fact[n-i]%mod;
    for(int i=k;i<=n;i++)
        (ans+=1ll*((i-k)%2?(mod-1):1)*C(i,k)%mod*F[i]%mod)%=mod;
    printf("%d\n",ans);
    return 0;
}
```

### CF285E

```cpp
#include <bits/stdc++.h>
#define int long long
using namespace std;
typedef pair<int,int> pi;
typedef long long ll;
inline int gin() {
    int s=0,f=1;
    char c=getchar();
    while(c<'0' || c>'9') {
        if(c=='-') f=-1;
        c=getchar();
    }
    while(c>='0'&&c<='9') {
        s=(s<<3)+(s<<1)+(c^48);
        c=getchar();
    }
    return s*f;
}

const int N=1005,mod=1e9+7;
int n,m,f[N][N][2][2],F[N];
int inv[N],fact[N],finv[N];

void init() {
    inv[1]=1;
    for(int i=2;i<=1000;i++) inv[i]=1ll*(mod-mod/i)*inv[mod%i]%mod;
    fact[0]=finv[0]=1;
    for(int i=1;i<=1000;i++) {
        fact[i]=1ll*fact[i-1]*i%mod;
        finv[i]=1ll*finv[i-1]*inv[i]%mod;
    }
}

int C(int n,int m) {
    if(m<0 || m>n) return 0;
    return 1ll*fact[n]*finv[m]%mod*finv[n-m]%mod;
}

signed main() {
    #ifndef ONLINE_JUDGE
    freopen("test.in","r",stdin);
    freopen("test.out","w",stdout);
    #endif
    init();
    n=gin(),m=gin();
    f[1][0][0][0]=f[1][1][0][1]=1;
    for(int i=2;i<n;i++) {
        f[i][0][0][0]=1;
        for(int j=1;j<=i;j++) {
            //i完美
            (f[i][j][0][0]+=f[i-1][j-1][0][0])%=mod;
            (f[i][j][1][0]+=f[i-1][j-1][0][1])%=mod;
            (f[i][j][0][1]+=f[i-1][j-1][0][0]+f[i-1][j-1][1][0])%=mod;
            (f[i][j][1][1]+=f[i-1][j-1][0][1]+f[i-1][j-1][1][1])%=mod;
            //i不完美
            (f[i][j][0][0]+=f[i-1][j][0][0]+f[i-1][j][1][0])%=mod;
            (f[i][j][1][0]+=f[i-1][j][0][1]+f[i-1][j][1][1])%=mod;
        }
    }
    //单独考虑第n位
    f[n][0][0][0]=1;
    for(int i=1;i<=n;i++) {
        (f[n][i][0][0]+=f[n-1][i-1][0][0]+f[n-1][i][0][0]+f[n-1][i][1][0])%=mod;
        (f[n][i][1][0]+=f[n-1][i-1][0][1]+f[n-1][i][0][1]+f[n-1][i][1][1])%=mod;
    }
    for(int i=0;i<=n;i++) F[i]=(f[n][i][0][0]+f[n][i][1][0])*fact[n-i]%mod;
    int ans=0;
    for(int i=m;i<=n;i++)
        (ans+=((i-m)%2?(mod-1):1)*C(i,m)%mod*F[i]%mod)%=mod;
    printf("%lld\n",ans);
    return 0;
}
```