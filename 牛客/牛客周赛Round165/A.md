- # **题目链接：**

[A-小月的dx分_牛客周赛 Round 165](https://ac.nowcoder.com/acm/contest/141721/A)

- # **题目描述：**

在某音乐游戏中，每次判定的结果分为 Critical Perfect、Perfect、Great、Good、Miss 五类，计分规则如下：

- 每次 Critical Perfect 计 3 分；
- 每次 Perfect 计 2 分；
- 每次 Great 计 1 分；
- 每次 Good 或 Miss 计 0 分。

一首歌的 DX 分等于所有判定对应分数的总和。 给定一首歌五类判定的数量，请计算它的 DX 分。

## 输入描述

在一行上输入五个整数 \(a,b,c,d,e\ (0 \le a,b,c,d,e \le 1000;\ a+b+c+d+e \le 1000)\)，分别表示 Critical Perfect、Perfect、Great、Good、Miss 的数量。

## 输出描述

输出一个整数，表示这首歌的 DX 分。

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
     ll a,b,c,d,e;cin>>a>>b>>c>>d>>e;
     cout<<(3*a+2*b+c);
     return 0;
 }
 ```

