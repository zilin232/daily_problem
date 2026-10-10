- # **题目链接：**

[求树的根_牛客题霸_牛客网](https://www.nowcoder.com/practice/e5a97317b37d46dcb10dd5dce66a2ec4?channelPut=tracker2)

- # **题目描述：**

给定一棵包含 n 个节点的有根树，节点编号为 \(1 \sim n\)。输入以 \(n-1\) 条有向边 \((a_i,b_i)\) 表示：存在一条从 \(a_i\) 指向 \(b_i\) 的边，且整棵图构成一棵树。

请输出：

- 树的根节点编号（唯一，入度为 0）；
- 所有叶子节点编号（出度为 0），按升序排列。

## 输入描述

第一行输入整数 \(n\ (1 \le n \le 10^5)\)。 接下来 \(n-1\) 行，每行输入两个整数 \(a_i,b_i\ (1 \le a_i,b_i \le n)\)，表示一条有向边 \(a_i \to b_i\)。

## 输出描述

第一行输出根节点编号。 第二行输出所有叶子节点编号（升序，空格分隔）。

- # **题目题解：**

 ```cpp
 #include<bits/stdc++.h>
 using namespace std;
 using ll=long long;
 using ull=unsigned long long;
 using ill=__int128;
 const ll mod1=1e9+7;
 const ll mod2=998244353;
 int main(){
     ios::sync_with_stdio(false);
     cin.tie(0);cout.tie(0);
     ll n;cin>>n;
     vector<ll>r(n+1,0);
     vector<ll>c(n+1,0);
     vector<ll>ans;
     for(ll i=1;i<n;i++){
         ll a,b;cin>>a>>b;
         r[b]++;c[a]++;
     }
     ll an=0;
     for(ll i=1;i<=n;i++){
         if(r[i]==0&&an==0)an=i;
         if(c[i]==0)ans.push_back(i);
     }
     cout<<an<<'\n';
     for(ll i:ans)cout<<i<<' ';
     return 0;
 }
 ```

