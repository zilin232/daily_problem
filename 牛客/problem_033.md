- # **题目链接：**

[sum_牛客题霸_牛客网](https://www.nowcoder.com/practice/139f0d4b353a48cbac0682214555753d?channelPut=tracker2)

- # **题目描述：**

 n 个数 \(a_i\)，你可以进行若干次修改操作，每一次操作任意修改一个数的值为 \(x(-10^4 \le x \le 10^4)\)。

问最少多少次操作使得这 n 个数的和为 sum。

## 输入描述

第一行输入一个整数 \(T(1 \le T \le 10^4)\)，表示测试数据组数。接下来是 T 个测试用例。

每个测试用例第一行包含两个整数 \(n, sum(1 \le n \le 2 \times 10^5,-n \times 10^4 \le sum \le n \times 10^4)\)。

每个测试用例第二行包含 n 个整数 \(a_i(-10^4 \le a_i \le 10^4)\)。

保证所有测试用例 n 的和不超过 \(2 \times 10^5\)。

## 输出描述

对于每个测试用例，输出一行，包含一个整数，表示答案。

可以证明，在数据范围的限制下，一定有一种操作方案满足条件。

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
         ll n,sum;cin>>n>>sum;
         ll su=0;
         vector<ll>a(n,0);
         for(ll i=0;i<n;i++)cin>>a[i],su+=a[i];
         if(su==sum){cout<<0<<'\n';continue;}
         sort(a.begin(),a.end());
         ll k=1;
         if(su>sum)for(ll i=1;i<=(n/2);i++)swap(a[i-1],a[n-i]),k=-1;
         ll p=abs(su-sum);
         ll ans=0;
         ll x=k*(ll)10000;
         for(ll i=0;i<n;i++){
             ans++;
             if(abs(x-a[i])>=p)break;
             p-=abs(x-a[i]);
         }
         cout<<ans<<'\n';
     }
     return 0;
 }
 ```

