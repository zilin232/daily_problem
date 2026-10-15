- # **题目链接：**

[B-小月的配对_牛客周赛 Round 165](https://ac.nowcoder.com/acm/contest/141721/B)

- # **题目描述：**

给定长度为 n 的排列 \(p_1,p_2\dots,p_n\) 与正整数 k。 对于 \(i\in[1,n]\)，请你统计满足 \(i+p_i\) 能够被 k 整除的 i 的数量。

【名词解释】 长度为 n 的排列：由 \(1,2,\dots,n\) 这 n 个整数、按任意顺序组成的数组（每个整数均恰好出现一次）。例如，\(\{2,3,1,5,4\}\) 是一个长度为 5 的排列，而 \(\{1,2,2\}\) 和 \(\{1,3,4\}\) 都不是排列，因为前者存在重复元素，后者包含了超出范围的数。

## 输入描述

第一行输入两个整数 \(n,k\ (1 \le n \le 2\times 10^5;\ 1 \le k \le 10^9)\)。 第二行输入 n 个整数 \(p_1,p_2,\dots,p_n\ (1 \le p_i \le n)\)。

## 输出描述

输出合格位置数量。

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
     ll n,k;cin>>n>>k;
     ll ans=0;
     for(ll i=1;i<=n;i++){
         ll p;cin>>p;
         if((i+p)%k==0)ans++;
     }
     cout<<ans;
     return 0;
 }
 ```

