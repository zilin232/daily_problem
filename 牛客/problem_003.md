- # **题目链接：**

  [好好好数_牛客题霸_牛客网](https://www.nowcoder.com/practice/503625f14bb24fe08fc508b872f48dae?channelPut=tracker2)

- # **题目描述：**

  小苯有一个数字 n，他定义 k- 好数为：可以表示为若干个不同的 k的整数次幂之和的数字。

  例如：30=3^3+3^1 ，因此 30是一个 3-好数，而 2不是一个 3-好数（虽然有：2=3^0+3^0，但好数要求次幂数字不同）。
  小苯有一个整数 n，他想知道 n最少可以被表示成几个 k-好数的和，请你帮帮他吧。

  ### 输入描述：

   每个测试文件均包含多组测试数据。第一行输入一个整数 T(1≤T≤1e4) 代表数据组数，每组测试数据描述如下：

   在一行上输入两个整数 n,k (1≤n≤1e18) , (1≤k≤1e18) ，表示小苯的数字 n、k-好数的 k。

  ### 输出描述：

  在一行上输出一个整数，代表最少可以将 n分解成 k-好数的个数。

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
     int t;cin>>t;
     while(t--){
         ll n,k;cin>>n>>k;
         if(n<k)cout<<n<<'\n';
         else{
             if(k==1)cout<<1<<'\n';
             else{
                 ll maxl=0;
                 while(n){
                     maxl=max(maxl,n%k);
                     n=n/k;
                 }
                 cout<<maxl<<'\n';
             }
         }
     }
     return 0;
 }
 ```

