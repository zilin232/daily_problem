- # **题目链接：**

[k - 路径（easy vension）_牛客题霸_牛客网](https://www.nowcoder.com/practice/7cda5b8060cc4c718847b9c06c72ef5c?channelPut=tracker2)

- # **题目描述：**

给定一颗 n 个点的无根树，每个节点有类型和权值，分别用 c 和 w 表示。一条简单路径的权值为这条路径包含的节点权值之和。

假设一条简单路径至少经过一个类型为 k 的节点，那么这条路径是 k- 路径。

对于所有的 \(k=1,2,3,\dots,n\)，输出一个整数，表示所有 k- 路径的最大权值，假如不存在，输出 \(-1\)。

提示：本题输入输出数据量较大，建议选手使用快速的输入输出方式。

## 输入描述

第一行输入一个整数 \(T(1 \le T \le 10^4)\)，表示测试数据组数。接下来是 T 个测试用例。

每个测试用例第一行输入一个整数 \(n(1 \le n \le 10^6)\)。

第二行有 n 个数 \(c_i(1 \le c_i \le n)\)，表示每个节点的类型。

第三行有 n 个数 \(w_i(-10^9 \le w_i \le 10^9)\)，表示每个节点的权值。

然后 \(n-1\) 行，每一行有两个整数 \(u,v\)，表示有一条 u 到 v 的无向边。

保证所有测试用例 n 的和不超过 \(10^6\)。

## 输出描述

对于每个测试用例，输出一行，包含 n 个空格分隔的整数，表示答案。

- # **题目题解：**

 ```cpp
 #include<bits/stdc++.h>
 using namespace std;
 using ll=long long;
 using ull=unsigned long long;
 using ill=__int128;
 const ll mod1=1e9+7;
 const ll mod2=998244353;
 ll c[1000010];
 ll w[1000010];
 vector<pair<ll,ll>> d[1000010];
 ll dfs(ll u,ll i){
     if(d[u][i].second!=-1e18)return d[u][i].second;
     ll p=d[u][i].first;
     ll x=0;
     for(ll j=0;j<d[p].size();j++){
         if(d[p][j].first==u)continue;
         x=max(x,dfs(p,j));
     }
     d[u][i].second=w[p]+x;
     return d[u][i].second;
 }
 int main(){
     ios::sync_with_stdio(false);
     cin.tie(0);cout.tie(0);
     ll t;cin>>t;
     while(t--){
         ll n;cin>>n;
         for(ll i=1;i<=n;i++)cin>>c[i];
         for(ll i=1;i<=n;i++)cin>>w[i];
         for(ll i=1;i<n;i++){
             ll u,v;cin>>u>>v;
             d[u].push_back({v,-1e18});
             d[v].push_back({u,-1e18});
         }
         for(ll i=1;i<=n;i++){
             for(ll j=0;j<d[i].size();j++){
                 d[i][j].second=dfs(i,j);
             }
         }
         for(ll i=1;i<=n;i++)sort(d[i].begin(),d[i].end(),[](pair<ll,ll>x,pair<ll,ll>y){return x.second>y.second;});
         vector<ll>ans(n+1,-1e18);
         for(ll i=1;i<=n;i++){
             if(d[i].size()>=2)ans[c[i]]=max(ans[c[i]],w[i]+max((ll)0,d[i][0].second)+max(d[i][1].second,(ll)0));
             else if(d[i].size()==1)ans[c[i]]=max(ans[c[i]],w[i]+max((ll)0,d[i][0].second));
             else ans[c[i]]=max(ans[c[i]],w[i]);
         }
         for(ll i=1;i<=n;i++){
             if(ans[i]==-1e18)cout<<-1<<' ';
             else cout<<ans[i]<<' ';
         }cout<<'\n';
         for(ll i=1;i<=n;i++)d[i].clear();
     }
     return 0;
 }
 //
 ```

