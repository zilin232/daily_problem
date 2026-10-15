- # **题目链接：**

[最大面积_牛客题霸_牛客网](https://www.nowcoder.com/practice/33c2a9cea6b344a6866d27a0c913fdd7?channelPut=tracker2)

- # **题目描述：**

牛牛有两个矩形，这两个矩形放在一个 yOx 坐标系内，且矩形的四条边均与坐标轴平行。

规定与 x 轴平行的边为矩形长，与 y 轴平行的边为矩形高。

矩形 1 的长与高分别为 \(a,b\)，矩形 2 的长与高分别为 \(c,d\)，牛牛现在想随意摆放这两个矩形，但不能改变这两个矩形的长与高，他想知道这两个矩形最大的相交面积是多大？

## 输入描述

一行四个整数 \(a,b,c,d(1 \le a,b,c,d \le 10^6)\)，前两个整数表示矩形 1 的长与高，后两个整数表示矩形 2 的长与高。

## 输出描述

一个整数，表示这两个矩形最大的相交面积。

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
     ll a,b,c,d;cin>>a>>b>>c>>d;
     cout<<(min(a,c)*min(b,d));
     return 0;
 }
 ```

