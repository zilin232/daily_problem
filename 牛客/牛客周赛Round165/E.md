- # **题目链接：**

[E-小月的折返颜色_牛客周赛 Round 165](https://ac.nowcoder.com/acm/contest/141721/E)

- # **题目描述：**

小月有一棵包含 n 个节点的树，节点的颜色用数组 \(c_1,c_2,\dots,c_n\) 表示，节点 i 的颜色为 \(c_i\)。

对于两个不同的节点 \(u,v\)，依次记录从 u 到 v 的简单路径上的所有节点。对于一条简单路径，每存在两个相邻节点的颜色不同，就记为一次换色。

请统计有多少个无序节点对 \(\{u,v\}\) 满足：\(c_u = c_v\)，并且它们之间的路径恰好换色两次。无序节点对 \(\{u,v\}\) 与 \(\{v,u\}\) 视为同一个节点对。

【名词解释】 简单路径：树上任意两个节点之间的路径，不经过重复的点和边。在树上，任意两个节点间有且仅有一条简单路径。

## 输入描述

第一行输入一个整数 \(n\ (1 \le n \le 2\times 10^5)\)，表示节点数量。 第二行输入 n 个整数 \(c_1,c_2,\dots,c_n\ (1 \le c_i \le n)\)，表示各节点的颜色。 此后 \(n-1\) 行，每行输入两个整数 \(u_i,v_i\ (1 \le u_i,v_i \le n;\ u_i \neq v_i)\)，表示一条连接节点 \(u_i\) 和 \(v_i\) 的边。保证给出的是一棵树。

## 输出描述

输出一个整数，表示满足条件的无序节点对数量。

- # **题目题解：**

 ```cpp
 #include<bits/stdc++.h>
 using namespace std;
 using ll=long long;
 using ull=unsigned long long;
 using ill=__int128;
 const ll mod1=1e9+7;
 const ll mod2=998244353;
 ll fa[200020];
 ll nm[200020];
 ll c[200020];
 ll n;
 ll find(ll x){
     return fa[x]!=x ? find(fa[x]):x;
 }
 void me(ll x,ll y){
     ll fx=find(x),fy=find(y);
     if(fx==fy)return;
     fa[fx]=fy;
     nm[fy]+=nm[fx];
 }
 int main(){
     ios::sync_with_stdio(false);
     cin.tie(0);cout.tie(0);
     cin>>n;
     for(ll i=1;i<=n;i++)cin>>c[i],fa[i]=i,nm[i]=1;
     vector<pair<ll,ll>>d;
     for(ll i=1;i<n;i++){
         ll u,v;cin>>u>>v;
         if(c[u]==c[v])me(u,v);
         d.push_back({u,v});
     }
     vector<vector<ll>>p(n+1);
     for(auto [u,v]:d){
         ll fx=find(u),fy=find(v);
         if(fx==fy)continue;
         p[fx].push_back(fy);
         p[fy].push_back(fx);
     }
     ll ans=0;
     vector<ll>num(n+1,0);
     for(ll i=1;i<=n;i++){
         for(auto j:p[i]){
             ans=ans+num[j]*nm[j];
             num[j]+=nm[j];
         }
         for(auto j:p[i])num[j]=0;
     }
     cout<<ans;
     return 0;
 }
 ```

