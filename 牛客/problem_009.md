- # **题目链接：**

[完美异或_牛客题霸_牛客网](https://www.nowcoder.com/practice/df2d0b1e250b4995a7cda77bf1065cf1?channelPut=tracker2)

- # **题目描述：**

给定一个长度为 n 的数组 \(\{a_1,a_2,\dots,a_n\}\)，如果满足以下两条性质，则称其为**伟大数组**：

1. 数组单调非降，且所有元素都是非负整数；
2. 其异或和 \(\bigoplus_{i=1}^{n} a_i\) 是 n 的一个因子，即 \(n \pmod{\bigoplus_{i=1}^{n} a_i} = 0\)。

现在给定整数 n，请你构造一个长度为 n 的伟大数组，或者判断不存在这样的数组。

## 名词解释

- 按位异或：xor 表示按位异或运算，运算方法为对两个整数的对应二进制位进行比较：若两位相同则结果为 0，不同则结果为 1。
- 异或和：\(\bigoplus_{i=1}^{n} a_i\) 表示将所有 \(a_i\) 依次按位异或得到的结果。

# 输入描述

每个测试文件均包含多组测试数据。第一行输入一个整数 \(T\ (1 \le T \le 10^4)\) 代表数据组数，每组测试数据描述如下：

在一行上输入一个整数 \(n\ (1 \le n \le 2 \times 10^5)\) —— 需要构造的数组长度。

除此之外，保证单个测试文件的 n 之和不超过 \(2 \times 10^5\)。

# 输出描述

对于每一组测试数据：

- 如果存在伟大数组，请在一行上按照非递减顺序输出 n 个整数 \(a_1,a_2,\dots,a_n\ (0 \le a_i \le 10^{18})\)；
- 如果不存在伟大数组，直接输出一个整数 \(-1\)。

如果存在多种可行答案，你可以输出任意一种即可，系统会自动判定是否正确。

- # **题目题解：**

n为偶数时，将这n个数分成1 3和n-2个1 ，1^3=2,偶数个1异或是0，0^2=2,是任意偶数的因数

n为奇数时，输出n个1，1是任意数的因数

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
     int t;cin>>t;
     while(t--){
         ll n;cin>>n;
         if(n&1)for(ll i=1;i<=n;i++)cout<<1<<' ';
         else{
             cout<<1<<' ';
             for(ll i=3;i<=n;i++)cout<<1<<' ';
             cout<<3;
         }
         cout<<'\n';
     }
     return 0;
 }
 ```

