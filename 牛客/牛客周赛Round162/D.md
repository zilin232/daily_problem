- # **题目链接：**

[D-小月的字带_牛客周赛 Round 162](https://ac.nowcoder.com/acm/contest/140489/D)

- # **题目描述：**

小月有一个字带，最初字带上的字符串只包含一个字符 \(c_0\)。 她会进行 n 次复制操作，用字符序列 \(c_1,c_2,\dots,c_n\) 表示，第 i 次复制的流程为：

- 设本次复制开始时字带上的字符串为 s；
- 设将 s 左右翻转后得到字符串 \(s'\)；
- 将字带上的字符串替换为 \(sc_is'\)，也就是将 s，\(c_i\)，\(s'\) 按顺序拼接后得到的字符串。

例如，字带为 \(\boldsymbol{ab}\)，本轮字符为 \(\boldsymbol{d}\) 时，复制后字带上的字符串会被替换为 \(\boldsymbol{abdba}\)。

请你计算，完成全部复制后，字带上的字符串中有多少对相同的相邻字符？

## 输入描述

第一行依次输入一个整数和一个小写字母 \(n,c_0\ (0 \le n \le 60)\)，表示复制轮数、初始字符。 第二行输入 n 个小写字母 \(c_1,c_2,\dots,c_n\)，表示各轮使用的字符。若 \(n = 0\)，则输入不存在第二行。

## 输出描述

输出一个整数，表示最终字带中相邻相同字符对的数量。

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
     ll n;char c0;cin>>n>>c0;
     if(n==0)cout<<0;
     else{
         vector<char>c(n);
         ll ans=0;
         char p=c0;
 //无论操作几次，最外面的字符一定是C0，所以每进行一次操作，就ans=ans*2,同时判断新中心是否和C0相同，相同再加2.
         for(ll i=0;i<n;i++){
             cin>>c[i];
             ans=ans*2;
             if(c[i]==p)ans+=2;
         }
         cout<<ans;
     }
     return 0;
 }
 ```

