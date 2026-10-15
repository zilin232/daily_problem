- # **题目链接：**

[C-小月的程序_牛客周赛 Round 165](https://ac.nowcoder.com/acm/contest/141721/C)

- # **题目描述：**

小月是一名黑客。当前终端上有一行长度为 n 的数据流，从左到右依次为 \(a_1,a_2,\dots,a_n\)。

小月拥有一个黑客程序，可以对数据流执行一次如下操作：选择一个位置 \(k\ (1 \le k \le n)\)，将数据流前 k 个元素的顺序完全反转，使数据流变为

\(a_k,a_{k-1},\dots,a_1,a_{k+1},\dots,a_n\)

设操作后的数组变为 \(b_1,b_2,\dots,b_n\)，为了维持系统的隐匿性，操作后的数据流必须满足 \(b_1 \le b_2 \le \dots \le b_n\)。满足条件的 k 被称为合格参数。

请你帮助小月计算，合格参数 k 的数量。

## 输入描述

每个测试文件均包含多组测试数据。第一行输入一个整数 \(T\ (1 \le T \le 10^4)\)，表示测试数据组数。对于每组测试数据：

第一行输入一个整数 \(n\ (1 \le n \le 2\times 10^5)\)，表示数据流长度。 第二行输入 n 个整数 \(a_1,a_2,\dots,a_n\ (-10^9 \le a_i \le 10^9)\)，表示数据流中的元素。

除此之外，保证单个测试文件中所有测试数据的 n 之和不超过 \(2\times 10^5\)。

## 输出描述

对于每组测试数据，在一行上输出一个整数，表示合格参数的数量。

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
     ll t;cin>>t;
     while(t--){
         ll n;cin>>n;
         vector<ll>a(n+2);
         for(ll i=1;i<=n;i++)cin>>a[i];
         if(n==1)cout<<1<<'\n';
         else{
             ll pr=1;
             for(ll i=2;i<=n;i++){
                 if(a[i]<=a[i-1])pr=i;
                 else break;
             }
             ll su=n;
             for(ll i=n-1;i>=1;i--){
                 if(a[i]<=a[i+1])su=i;
                 else break;
             }
             ll l=max((ll)1,su-1);
             ll r=pr;
             ll ans=0;
             for(ll k=l;k<=min(r,n-1);k++){
                 if(a[1]<=a[k+1])ans++;
             }
             if(r>=n)ans++;
             cout<<ans<<'\n';
         }
     }
     return 0;
 }
 
 ```

