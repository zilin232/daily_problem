- # **题目链接：**

[F-小月的树_牛客周赛 Round 162](https://ac.nowcoder.com/acm/contest/140489/F)

- # **题目描述：**

小月有一棵包含 n 个节点的树，节点的颜色用一个长为 n 的字符串 \(s = s_1s_2\dots s_n\ (s_i \in \{\text{B},\text{R}\})\) 表示，B 表示蓝色，R 表示红色，i 号节点的颜色为 \(s_i\)。

她要选择一个**非空且连通**的节点集合，将集合内的节点以及与这些节点相连的边全部删除。 她希望删除后，每一个剩余连通块内的所有节点颜色都相同。特殊的，若删除后图为空，则视为满足条件。 请你求出她至少需要删除多少个节点。

【名词解释】 **连通**：若该节点集合在原树上诱导的子图连通，则称这个集合连通。等价地，集合中任意两个顶点之间在树上的简单路径上的所有顶点都属于该集合。

**连通块**：也称连通分量，满足：

- 是所在图的一个子图；
- 连通块内的任意两个顶点之间都存在路径相连，且路径上的点也在连通块内；
- 是极大的，即不能再通过添加所在图中的其他顶点而依旧保持连通性； 单独的点也构成一个连通块。

## 输入描述

第一行输入一个整数 \(n\ (1 \le n \le 2 \times 10^5)\)，代表树的节点数量。 第二行输入一个长度为 n、仅由 \(\text{R}\) 和 \(\text{B}\) 组成的字符串 s。 之后的 \(n-1\) 行，第 i 行输入两个整数 \(u_i,v_i\ (1 \le u_i,v_i \le n;\ u_i \ne v_i)\) 表示树上第 i 条边连接节点 \(u_i\) 和 \(v_i\)。保证树连通。

## 输出描述

输出一个整数，代表最少需要删除的节点数量。

- # **题目题解：**

 ```cpp
 #include<bits/stdc++.h>
 using namespace std;
 using ll=long long;
 using ull=unsigned long long;
 using ill=__int128;
 const ll mod1=1e9+7;
 const ll mod2=998244353;
 vector<ll>d[200020];
 ll is[200020];
 ll an[200020];//以i为根节点的is数量
 ll p[200020];//是不是 可能是可被删区域
 ll dfs(ll fa,ll x){
     an[x]=is[x];
     for(auto v:d[x]){
         if(v==fa)continue;
         an[x]+=dfs(x,v);
     }
     return an[x];
 }
 int main(){
     ios::sync_with_stdio(false);
     cin.tie(0);cout.tie(0);
     ll n;cin>>n;string s;cin>>s;
     s=' '+s;
     for(ll i=1;i<n;i++){
         ll u,v;cin>>u>>v;
         d[u].push_back(v);
         d[v].push_back(u);
         if(s[u]!=s[v])is[u]+=1,is[v]+=1;//记录两点不同
     }
     ll ro=-1;
     //找根，因为只有n-1个边，所以必然有一个点的出度是1
     for(ll i=1;i<=n;i++){
         if(d[i].size()==1){
             ro=i;break;
         }
     }
     dfs(-1,ro);
     for(ll i=1;i<=n;i++)p[i]=1;
     for(ll i=1;i<=n;i++){
         if(an[i]==0||an[i]==an[ro]){
      //在被删区域的下面和被删区域的上面
             p[i]=0;
         }
     }
     for(ll i=1;i<=n;i++)if(is[i])p[i]=1;//一开始就被标记了
     ll ans=0;
     for(ll i=1;i<=n;i++){
         if(!p[i])continue;//一定不是被删区域
         ans++;
         //判断是不是只连了一个is，是的话该节点不用被删
         ll an=0;
         for(auto v:d[i]){
             if(p[v])an++;
         
         if(an==1)ans--;
     }
     if(ans==0)ans++;
     //最小删一个（题目要求）
     cout<<ans;
     return 0;
 }
 ```

