- # **题目链接：**

[小绿的房子_牛客题霸_牛客网](https://www.nowcoder.com/practice/dfab1015071f4d37b4f6e174b447c7c0?channelPut=tracker2)

- # **题目描述：**

大白熊给了小苯一个长度为 n 的数组 a，他希望小苯将数组 a 变成有序（非递减）的。具体的，小苯需要进行如下操作：

1. 任选一个数组 b，长度也为 n，且元素满足：\(-10^{10} \le b_i \le 10^{10}\)。
2. 对于所有 \(1 \le i \le n\)，都执行 \(a_i = a_i + b_i\)。

大白熊希望在执行完操作后 a 数组满足有序，同时要最小化数组 b 的极差，即使得：

\(\max(b_1,b_2,\dots,b_n) - \min(b_1,b_2,\dots,b_n)\) 最小。

请你帮小苯找出一个合法的 b 数组吧。

注：如有多解输出任意即可。

## 输入描述

输入包含两行。 第一行一个正整数 \(n(1 \le n \le 2 \times 10^5)\)，表示 a 的长度。 第二行 n 个整数 \(a_i(-10^9 \le a_i \le 10^9)\)，表示数组 a 的元素。

## 输出描述

输出包含一行 n 个整数，表示构造出的 b 数组（有多解输出任意即可）。 如果找不到合法的 b 数组，请输出一个整数 \(-1\)。

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
     vector<vector<ll>>d(n+1);
     for(ll i=1;i<n;i++){
         ll u,v;cin>>u>>v;
         d[u].push_back(v);
         d[v].push_back(u);
     }
     ll ans=0;
     vector<ll>is(n+1,0);//有多少个非叶子节点相连
     vector<ll>nm(n+1,0);//非叶子节点是哪个
     for(ll i=1;i<=n;i++){
         for(auto j:d[i]){
             if(d[j].size()>1){
                 is[i]++;
                 nm[i]=j;
             }
         }
     }
     for(ll i=1;i<=n;i++){
         bool f=true;
         for(auto j:d[i]){
             if(is[j]>1||(is[j]==1&&i!=nm[j])){
                 f=false;break;
             }
         }//如果节点i，至少有一个相连节点的相连非叶子节点数量大于1 或 至少有一个相连节点的相连非叶子节点数量是1但相连的的非叶子节点不是i，那么至少会有一个节点和i的距离会大于2.
         if(f){ans++;}
     }
     cout<<ans;
     return 0;
 }
 ```

