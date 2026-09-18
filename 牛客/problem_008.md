- # **题目链接：**

[核心信任者_牛客题霸_牛客网](https://www.nowcoder.com/practice/6283453737754229a17ccb19b406afb5?channelPut=tracker2)

- # **题目描述：**

在某公司内有 N 名员工，编号为 \(1 \sim N\)。每位员工默认信任自己，也可能信任其他同事；信任关系具有**传递性**—— 若员工 A 信任员工 B，且员工 B 信任员工 C，则 A 也信任 C。

我们称：如果所有员工都信任员工 i，则该员工为**核心信任者**。

现给定 M 条直接信任关系，请计算可以成为核心信任者的员工数量。

## 名词解释

- 传递性：如果 A 信任 B 且 B 信任 C，则 A 也信任 C。
- 核心信任者：若所有员工都信任员工 i，则称该员工为核心信任者。
- 直接信任关系：员工 A 信任员工 B，表示 A 信任 B。

## 输入描述

第一行输入两个整数 \(N, M \ (1 \le N \le 10^5,\ 1 \le M \le 5 \times 10^5)\)，分别表示员工数量与直接信任关系数量。

接下来 M 行，每行输入两个整数 \(A, B \ (1 \le A,B \le N)\)，表示员工 A 信任员工 B。

## 输出描述

输出一个整数，表示可以成为核心信任者的员工总数。

- # **题目题解：**

  Tarjan算法的模板题
  用Tarjan进行SCC缩点之后检查出度为0(或者入度，取决于建图方向)的SCC数量，如果只有1个就输出sccSize，否则就是0
  详细解释可以看这个https://www.doubao.com/thread/xcFiclOsaHI8LpEyo或者b站 左程云的视频

 ```cpp
 #include<bits/stdc++.h>
 using namespace std;
 using ll=long long;
 using ull=unsigned long long;
 using ill=__int128;
 const ll mod1=1e9+7;
 const ll mod2=998244353;
 const ll N=1e5+9;
 vector<ll>tu[N];
 ll a[N],b[N],c[N];
 stack<ll>ak;
 bool is[N];
 ll t,num;
 void tr(ll u){
     t++;
     a[u]=t;b[u]=t;
     ak.push(u);
     is[u]=true;
     for(auto v:tu[u]){
         if(a[v]==0){
             tr(v);
             b[u]=min(b[v],b[u]);
         }else if(is[v]){
             b[u]=min(b[u],a[v]);
         }
     }
     if(a[u]==b[u]){
         num++;
         ll p;
         do{
             p=ak.top();
             ak.pop();
             c[p]=num;
             is[p]=false;
         }while(p!=u);
     }
 }
 int main(){
     ios::sync_with_stdio(false);
     cin.tie(0);cout.tie(0);
     t=0;num=0;
     ll n,m;cin>>n>>m;
     for(ll i=1;i<=m;i++){
         ll u,v;cin>>u>>v;
         tu[u].push_back(v);
     }
     for(ll i=1;i<=n;i++){
         if(a[i]==0)tr(i);
     }
     vector<ll>p1(num+1,0);
     vector<ll>p2(num+1,0);
     for(ll i=1;i<=n;i++){
         p1[c[i]]++;
         for(auto v:tu[i]){
             if(c[v]!=c[i])p2[c[i]]++;
         }
     }
     ll cd=0,sl=0;
     for(ll i=1;i<=num;i++){
         if(p2[i]==0){
             cd++;
             sl=p1[i];
         }
     }
     if(cd==1)cout<<sl;
     else cout<<0;
     return 0;
 }
 ```

