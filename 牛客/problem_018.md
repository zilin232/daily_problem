- # **题目链接：**

[小红树_牛客题霸_牛客网](https://www.nowcoder.com/practice/31280814b0ec4675bef8884a6daf764d?channelPut=tracker2)

- # **题目描述：**

小红拿到了一棵树，每个节点被染成了红色或者蓝色。 小红定义每条边的权值为：删除这条边时，形成的两个子树的同色连通块数量之差的绝对值。 小红想知道，所有边的权值之和是多少？

## 输入描述：

第一行输入一个正整数n，代表节点的数量。 第二行输入一个长度为n且仅由 'R' 和 'B' 两种字符组成的字符串。第i个字符为 'R' 代表i号节点被染成红色，为 'B' 则被染成蓝色。 接下来的\(n-1\)行，每行输入两个正整数u和v，代表节点u和节点v有一条边相连。 \(1 \le n \le 200000\)

## 输出描述：

一个正整数，代表所有边的权值之和。

- # **题目题解：**

 ```cpp
 #include<bits/stdc++.h>
 using namespace std;
 using ll=long long;
 using ull=unsigned long long;
 using ill=__int128;
 const ll mod1=1e9+7;
 const ll mod2=998244353;
 const ll N=2e5+10;
 ll n;
 string s;
 vector<ll>a[N];
 ll nm[N];//以i为为根的子树的连通块数量
 ll ans;//权值之和
 void dfs1(ll x,ll fa){
     nm[x]=1;
     for(auto v:a[x]){
         if(v==fa)continue;
         dfs1(v,x);
         nm[x]+=nm[v];
         if(s[x]==s[v])nm[x]--;
     }
 }//第一遍dfs求nm[i]值
 void dfs2(ll x,ll fa){
     for(auto v:a[x]){
         if(v==fa)continue;
         dfs2(v,x);
         ll q=nm[1]-nm[v];
         if(s[v]==s[x])q++;
         ans=ans+abs(q-nm[v]);
     }
 }//第二遍的dfs求去每个边后的权值
 int main(){
     ios::sync_with_stdio(false);
     cin.tie(0);cout.tie(0);
     cin>>n;
     cin>>s;
     s='?'+s;
     for(ll i=1;i<n;i++){
         ll u,v;cin>>u>>v;
         a[u].push_back(v);
         a[v].push_back(u);
     }
     dfs1(1,-1);
     dfs2(1,-1);
     cout<<ans;
     return 0;
 }
 ```

