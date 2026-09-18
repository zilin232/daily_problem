- # **题目链接：**

[小红的区间构造_牛客题霸_牛客网](https://www.nowcoder.com/practice/df1bbce22cad4d2a8b69b7db3715e651?channelPut=tracker2)

- # **题目描述：**

小红拿到了正整数 x ，她希望你找到一个长度为 k的区间，满足区间内恰好有 n个数是 x的倍数。你能帮帮她吗？

### 输入描述：

在一行上输入三个整数 n,k,x(1≤n,k,x≤1e9) 。

### 输出描述：

如果答案不存在，直接输出 −1 ；否则，输出两个正整数 l,r(1≤l≤r<2×1e9; l+k−1=r)代表答案。

如果存在多个解决方案，您可以输出任意一个，系统会自动判定是否正确。注意，自测运行功能可能因此返回错误结果，请自行检查答案正确性。

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
     ll n,k,x;cin>>n>>k>>x;
     ll maxl=(k-1)/x+1;//k长度区间最多有多少
     ll minl=k/x;//k长度区间最少要多少
     //两者最多差一
     if(n<minl||n>maxl)cout<<-1;
     else{
         if(n==minl)cout<<1<<' '<<k;
     else cout<<x<<' '<<(x+k-1);
     //少的放后面，多的放前面
     }
     return 0;
 }
 ```

