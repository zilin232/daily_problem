- # **题目链接：**

[讨厌鬼进货_牛客题霸_牛客网](https://www.nowcoder.com/practice/e364bac751204aa0b2d27389ca8e3c94?channelPut=tracker2)

- # **题目描述：**

  讨厌鬼需要采购 n 种货物，每种货物可通过以下方式获取：

  - 在供应商 A 以 \(a_i\) 元购得第 i 种；
  - 在供应商 B 以 \(b_i\) 元购得第 i 种；
  - 在网购平台一次性购买全部 n 种，花费 x 元（不能拆分）。

  可以自由组合以上方式，只要最终每种货物都至少购买一件。求最小总花费。

  ## 输入描述

  第一行输入两个整数 \(n,x\ (1 \le n \le 10^5;\ 1 \le x \le 10^9)\)。 第二行输入 n 个整数 \(a_1,a_2,\dots,a_n\ (1 \le a_i \le 10^4)\)。 第三行输入 n 个整数 \(b_1,b_2,\dots,b_n\ (1 \le b_i \le 10^4)\)。

  ## 输出描述

  输出一个整数，表示完成采购的最少花费。

- # **题目题解：**

 ```cpp
 #include<bits/stdc++.h>
 using namespace std;
 using ll=long long;
 using ull=long long;
 using ill=__int128;
 const ll p=1e9+7;
 const ll q=998244353;
 int main(){
     ios::sync_with_stdio(false);
     cin.tie(0);cout.tie(0);
     int n,x;cin>>n>>x;
     int minl=0;
     vector<int>a(n);
     vector<int>b(n);
     for(int i=0;i<n;i++)cin>>a[i];
     for(int i=0;i<n;i++)cin>>b[i];
     for(int i=0;i<n;i++)minl+=min(a[i],b[i]);//每次买花费较少的
     cout<<min(minl,x);//和一次性购买比较
     return 0;
 }
 ```

