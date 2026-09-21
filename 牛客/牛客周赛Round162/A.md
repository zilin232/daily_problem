- # **题目链接：**

[A-小月的贴纸_牛客周赛 Round 162](https://ac.nowcoder.com/acm/contest/140489/A)

- # **题目描述：**

小月有 n 段纸带，每段纸带的两端各有一张贴纸。 她将这些纸带首尾相接拼成一条单链。在每个连接处，相邻两段纸带的贴纸会完全重叠，此时两张重叠的贴纸只能看见一张。 请计算拼接后最终能看见多少张贴纸。

## 输入描述

输入一个整数 \(n\ (1 \le n \le 100)\)，表示纸带的段数。

## 输出描述

输出一个整数，表示能看见的贴纸张数。

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
     //n个纸带有2*n个贴纸，接在一起有n-1个接点导致n-1位置的两个贴纸重叠，减去重叠的部分n-1.
     //输出n+1
     ll n;cin>>n;
     cout<<n+1;
     return 0;
 }
 ```

