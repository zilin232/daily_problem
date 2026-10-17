- # **题目链接：**

[加减_牛客题霸_牛客网](https://www.nowcoder.com/practice/b6aff86eef4f4622aec75154fbf183c7?channelPut=tracker2)

- # **题目描述：**

小红拿到了一个长度为 n 的数组。她每次操作可以让某个数加 1 或者某个数减 1。 小红最多能进行 k 次操作。她希望操作结束后，该数组出现次数最多的元素次数尽可能多。 你能求出这个最大的次数吗？

## 输入描述

第一行两个正整数 n 和 k 第二行有 n 个正整数 \(a_i\)

\(1 \le n \le 10^5\) \(1 \le k \le 10^{12}\) \(1 \le a_i \le 10^9\)

## 输出描述

不超过 k 次操作之后，数组中可能出现最多次数元素的次数。

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
     ll n,k;cin>>n>>k;
     vector<ll>a(n+1,0);
     for(ll i=1;i<=n;i++)cin>>a[i];
     sort(a.begin()+1,a.begin()+1+n);
     vector<ll>pr(n+1,0);
     for(ll i=1;i<=n;i++)pr[i]=pr[i-1]+a[i];
     ll maxl=0;
     for(ll i=1;i<=n;i++){
         ll l=i;
         ll rl=l,rr=n;
         //cout<<rl<<' '<<rr<<'\n';
         ll an=l;
         while(rl<=rr){
             ll r=(rl+rr)/2;
             //cout<<r<<' ';
             ll m1=(l+r)/2,m2=(l+r+1)/2;
             //cout<<m1<<' '<<m2<<' ';
             ll p1=pr[r]+pr[l]-2*pr[m1]-a[l]-(r+l-2*m1-1)*a[m1];
             ll p2=pr[r]+pr[l]-2*pr[m2]-a[l]-(r+l-2*m2-1)*a[m2];
             ll p=min(p1,p2);
             if(p>k)rr=r-1;
             else rl=r+1,an=max(r,an);
             //cout<<p<<' '<<rl<<' '<<rr<<'\n';
         }
         maxl=max(maxl,an-l+1);
         //cout<<rl<<' '<<l<<'\n';
         //cout<<"??????????"<<'\n';
     }
     cout<<maxl;
     return 0;
 }
 ```

