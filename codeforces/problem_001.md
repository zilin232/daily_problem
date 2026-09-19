- # **题目链接：**

[Problem - C - Codeforces](https://codeforces.com/contest/2264/problem/C)

- # **题目描述**：

time limit per test: 2 seconds memory limit per test: 256 megabytes

Madam Madamant is expecting a baby and already planning a skating dynasty in which every parent is a stronger skater than their children.

Formally, Madamant has n labeled skaters. Skater v has an integer rating \(a_v\), and all ratings are pairwise distinct. A possible dynasty is represented by a rooted tree on these skaters.

Let r be the root of the tree. For every skater \(v \neq r\), let \(p_v\) be the parent of v. The dynasty is valid if \(a_v < a_{p_v}\) for every \(v \neq r\). The cost of a valid dynasty is

\(\sum_{v\neq r}(a_{p_v}-a_v).\)

Two dynasties are different if their roots are different or if the parent of at least one skater is different.

Find the sum of the costs of all valid dynasties Madamant can form, modulo \(998\,244\,353\).

### Input

Each test contains multiple test cases. The first line contains the number of test cases \(t\ (1 \le t \le 10^4)\). The description of the test cases follows.

The first line of each test case contains a single integer \(n\ (1 \le n \le 2\cdot 10^5)\) — the number of skaters. The second line contains n integers \(a_1,a_2,\dots,a_n\ (1 \le a_i \le 10^9)\) — their ratings. It is guaranteed that all \(a_i\) are pairwise distinct. It is guaranteed that the sum of n over all test cases does not exceed \(2\cdot 10^5\).

### Output

For each test case, print one integer — the sum of the costs of all valid dynasties, modulo \(998\,244\,353\).

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
         ll n;cin>>n;
         vector<ll>a(n,0);
         for(ll i=0;i<n;i++)cin>>a[i];
         if(n==1){
             cout<<0<<'\n';
             continue;
         }
         sort(a.begin(),a.end(),[](ll x,ll y){
             return x>y;
         });//先从大到小排序便于后续处理。
         vector<ll>pre(n,0);//前缀和
         pre[0]=a[0];
         for(ll i=1;i<n;i++)pre[i]=(pre[i-1]+a[i])%mod2;
         ll ans=0;
         ll jc=1;
         //这里采用每多加一个更小的数q会给总值增加多少。
         for(ll i=1;i<n;i++){
             ll pjc=jc;
             jc=(jc*i)%mod2;
             ll k=(i*a[i])%mod2;
             ll p=((pre[i-1]-k)%mod2+mod2)%mod2;
             p=(p*pjc)%mod2;
             ans=((ans*i)%mod2+p)%mod2;
         }
         //由k到k+1个节点。
         //k个节点的方案数是 (k-1)！，对于任意一种方案 a,假设该方案的值是b。
         //将q新节点值加到a中，都有k种放法，这k种放法会多产生(k-1)*b+pre[k]-k*q;
         //所以加入q新节点值会增加(k-1)*ans+(k-1)!*(pre[k]-k*q);
         cout<<ans<<'\n';
     }
     return 0;
 }
```

