- # **题目链接：**

[炮兵阵地_牛客题霸_牛客网](https://www.nowcoder.com/practice/31a33330bc1e4b5ea91c08bc1c18aaf5?channelPut=tracker2)

- # **题目描述：**

 在一张 N×M的网格地图上（N 行、M 列），每个单元格为
∙ ∙ **P**：平原，可部署炮兵；
∙ ∙ **H**：山地，无法部署炮兵。

 一支炮兵部队部署在坐标 (r,c)(*r*,*c*) 后，可攻击同行左右各 2 格 (r,c±1),(r,c±2)(*r*,*c*±1),(*r*,*c*±2) 以及同列上下各 22 格 (r±1,c),(r±2,c)(*r*±1,*c*),(*r*±2,*c*)，如图所示：

![img](https://uploadfiles.nowcoder.com/images/20180701/305473_1530454615753_58BC0148FDF4BE2D4D3EDC671AD479A2)

 现需在保证**任何两支炮兵不能互相攻击**的前提下，最大化地图上炮兵部队的数量。求可部署的炮兵数量上限。

### 输入描述：

 第一行输入两个整数 N,M*N*,*M*。(1≦N≦100, 1≦M≦10)
 接下来的 N行，每行一个长度为 M的字符串，字符为 **P** 或 **H**，描述地图。

### 输出描述：

**注：**本题解来自 牛客的 “丨阿伟丨” 

输出一个整数 K，表示最多可部署的炮兵数量。

- # **题目题解：**

本题是又一个经典的棋盘类动态规划问题，解法仍然是***\*状态压缩DP\****。与“互不侵犯的国王”问题（[[SCOI2005\]互不侵犯KING](https://ac.nowcoder.com/acm/problem/20240)）相比，本题的核心区别在于炮兵的攻击范围更远，一个炮兵会影响到其上下两行，这使得 DP 的状态定义和转移变得更加复杂。

***\*核心思想\****：

由于第 i 行的决策会受到第 i-1 行和第 i-2 行的影响，因此我们的 DP 状态必须同时记录前两行的布局信息。

***\*1. 状态表示\****

我们定义一个三维 DP 数组： dp[i][j][k]

其含义是：***\*在处理完前\**** i ***\*行后，第\**** i ***\*行的布局为状态\**** j***\*，第\**** i-1 ***\*行的布局为状态\**** k ***\*时，能够部署的炮兵最大数量。\****

· i: 当前处理的行号（0-indexed）。

· j: 一个位掩码，表示第 i 行的布局。

· k: 一个位掩码，表示第 i-1 行的布局。

***\*2. 状态转移\**** dp[i][j][k] 的值，可以从所有与 j 和 k 兼容的、合法的 dp[i-1][k][p] 状态转移而来。这里 p 代表了第 i-2 行的布局。转移方程为：

dp[i][j][k] = max(dp[i-1][k][p]) + count(j)

其中，count(j) 是状态 j 中炮兵的数量（即二进制中 1 的个数）。这个转移需要满足一系列的约束条件：

**·** ***\*地形约束\****：炮兵不能部署在山地上。如果 map_state[i] 是第 i 行山地的位掩码，则 (j & map_state[i]) == 0。

**·** ***\*行内约束\****：同一行中，任意两个炮兵之间至少要间隔两个空格。位运算表示为 (j & (j << 1)) == 0 且 (j & (j << 2)) == 0。

**·** ***\*行间约束\****：

o 第 i 行与第 i-1 行不冲突：(j & k) == 0。

o 第 i 行与第 i-2 行不冲突：(j & p) == 0。

o （第 i-1 行与第 i-2 行不冲突 (k & p) == 0，这个条件在计算 dp[i-1][k][p] 时已经保证了）。

***\*3. 优化与实现\****

**·** ***\*预处理地形\****：将输入的字符地图 'P' 和 'H' 转换为一个整数数组 map_state，其中每个整数是一个位掩码，1 代表山地。

**·** ***\*预处理合法布局\****：我们可以预先找出所有满足***\*行内约束\****的布局状态，并计算好每个状态的炮兵数量，存入列表 states 和 counts。这可以显著减少 DP 过程中的状态空间。

**·** ***\*DP 数组 Padding\****：为了方便处理边界情况（i=0 和 i=1），我们可以给 DP 数组的行数增加一个 padding，例如定义 dp 表的大小为 (N+2) x |states| x |states|，其中 dp[i+2] 对应地图的第 i 行。这样 i=0 时，它会从 dp[1] 读取，而 dp[1] 和 dp[0] 都是初始的 0，逻辑上是通顺的，无需特殊处理边界。

***\*4. 最终答案\****

在填充完整个 DP 表格后，最终的答案是 dp[N+1]（对应处理完第 N-1 行）中的最大值。

 ```cpp
 #include<bits/stdc++.h>
 using namespace std;
 using ll=long long;
 using ull=unsigned long long;
 using ill=__int128;
 const ll mod1=1e9+7;
 const ll mod2=998244353;
 ll num1(ll n){
     ll ans=0;
     while(n){
         n=n&(n-1);
         ans++;
     }
     return ans;
 }
 int main(){
     ios::sync_with_stdio(false);
     cin.tie(0);cout.tie(0);
     ll n,m;cin>>n>>m;
     vector<ll>a(n+1,0);
     for(ll i=1;i<=n;i++){
         string s;cin>>s;
         for(ll j=0;j<m;j++){
             if(s[j]=='H')a[i]=a[i]|(1<<j);
         }
     }
     //cout<<m<<'\n';
     vector<ll>y;
     vector<ll>nm;
     for(ll i=0;i<(1<<m);i++){
         if(!(i&(i<<1)) && !(i&(i<<2))){
             y.push_back(i);
             nm.push_back(num1(i));
         }
     }
     ll q=y.size();
     //cout<<q<<'\n';
     vector<vector<vector<ll>>>dp(n+4,vector<vector<ll>>(q,vector<ll>(q,0)));
     for(ll i=1;i<=n;i++){
         ll a1=a[i];
         for(ll j=0;j<q;j++){
             ll a2=y[j];
             if(a1&a2)continue;
             ll nm1=nm[j];
             for(ll k=0;k<q;k++){
                 ll a3=y[k];
                 if(a2&a3)continue;
                 for(ll p=0;p<q;p++){
                     ll a4=y[p];
                     if(a4&a2)continue;
                     if(a4&a3)continue;
                     dp[i+2][j][k]=max(dp[i+2][j][k],dp[i+1][k][p]+nm1);
                 }
             }
         }
     }
     ll maxl=0;
     for(ll i=0;i<q;i++){
         for(ll j=0;j<q;j++){
             maxl=max(maxl,dp[n+2][i][j]);
             //cout<<dp[n+2][i][j]<<' ';
         }
         //cout<<'\n';
     }
     cout<<maxl;
     return 0;
 }
 ```

