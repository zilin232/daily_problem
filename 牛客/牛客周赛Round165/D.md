- # **题目链接：**

[D-小月的删数_牛客周赛 Round 165](https://ac.nowcoder.com/acm/contest/141721/D)

- # **题目描述：**

小月正在进行一个删数游戏。她获得了一个长度为 n 的整数数组 \(a_1,a_2,\dots,a_n\)。

她必须进行恰好一次操作：选择一个在数组中出现过的数值 c，删除数组中所有等于 c 的元素，其他元素的相对顺序保持不变。 删除后，将剩余的 m 个元素从 1 开始重新编号，得到数组 \(b_1,b_2,\dots,b_m\)。这个数组的读数定义如下：

- 若 \(m>0\)，读数为 \(b_1-b_2+b_3-\dots\)，即奇数下标处的元素之和减去偶数下标处的元素之和；
- 若 \(m=0\)，即所有元素均被删除，读数为 0。

小月想知道，选择不同的数值 c，能够得到的读数的绝对值最小是多少？

## 输入描述

第一行输入一个整数 \(n\ (1 \le n \le 2\times 10^5)\)，表示数组的长度。 第二行输入 n 个整数 \(a_1,a_2,\dots,a_n\ (-10^9 \le a_i \le 10^9)\)，表示数组中的元素。

## 输出描述

输出一个整数，表示能够得到的读数的绝对值的最小值。

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
     ll n;cin>>n;
     vector<ll>a(n,0);
     vector<ll>c(n,0);
     vector<ll>is(n,0);
     for(ll i=0;i<n;i++){cin>>a[i];c[i]=a[i];if(i&1)is[i]=-1;else is[i]=1;}
     vector<ll>pr(n,0);
     pr[0]=a[0];
     for(ll i=1;i<n;i++)pr[i]=pr[i-1]+a[i]*is[i];
     vector<ll>b;
     sort(c.begin(),c.end());
     b.push_back(c[0]);
     for(ll i=1;i<n;i++){
         if(c[i]!=c[i-1])b.push_back(c[i]);
     }
     ll minl=1e18;
     ll m=b.size();
     unordered_map<ll,vector<ll>>mp;
     for(ll i=0;i<n;i++)mp[a[i]].push_back(i);
     //cout<<m<<' ';
     //for(ll i=0;i<m;i++)cout<<b[i]<<' ';
     for(ll i=0;i<m;i++){
         ll an=pr[n-1];
         ll v=b[i];
         ll len=mp[v].size();
         for(ll j=0;j<len;j++){
             if(j%2==0){
                 ll p=pr[n-1]-pr[mp[v][j]];
                 an=an-2*p-a[mp[v][j]]*is[mp[v][j]];
             }else{
                 ll p=pr[n-1]-pr[mp[v][j]];
                 an=an+2*p+a[mp[v][j]]*is[mp[v][j]];
             }
         }
         an=abs(an);
         minl=min(minl,an);
     }
     cout<<minl;
     return 0;
 }
 ```

