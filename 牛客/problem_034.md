- # **题目链接：**

[小红的因式分解_牛客题霸_牛客网](https://www.nowcoder.com/practice/b4b3c3c193ad43e5bc66018b1141cdb3?channelPut=tracker2)

- # **题目描述：**

小红有三个整数 \(a,b,c\)，要将 \(ax^2+bx+c\) 分解为 \((a_1x+b_1)(a_2x+b_2)\) 的形式，其中 \(a_1,b_1,a_2,b_2\) 均为整数。

如果可以分解，请按 \(a_1,b_1,a_2,b_2\) 的顺序输出，若有多解输出任意一种，若无解，输出 `"NO"`。

## 输入描述

第一行输入一个整数 T，表示有 T 组测试数据。 接下来 T 行，每行输入三个整数 \(a,b,c\)。

\(1 \le T \le 100\) \(-10^6 \le a,b,c \le 10^6\) \(a \neq 0\)

## 输出描述

输出 T 行，每行输出四个整数 \(a_1,b_1,a_2,b_2\)，表示 \((a_1x+b_1)(a_2x+b_2)\) 的形式，若无解，输出 `"NO"`。

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
         ll n,b,m;cin>>n>>b>>m;
         if(m==0){
             ll a1=gcd(abs(n),abs(b));
             ll a2=n/a1;
             ll b2=b/a1;
             cout<<a1<<' '<<0<<' '<<a2<<' '<<b2<<'\n';
             continue;
         }
         vector<pair<ll,ll>>a;
         vector<pair<ll,ll>>c;
         ll aa=abs(n);ll cc=abs(m);
         for(ll i=1;i*i<=aa;i++){
             if(aa%i==0){
                 a.push_back({i,n/i});
                 a.push_back({-i,-n/i});
                 a.push_back({n/i,i});
                 a.push_back({-n/i,-i});
             }
         }
         for(ll i=1;i*i<=cc;i++){
             if(cc%i==0){
                 c.push_back({i,m/i});
                 c.push_back({-i,-m/i});
                 c.push_back({m/i,i});
                 c.push_back({-m/i,-i});
             }
         }
         bool f=false;
         for(auto [a1,a2]:a){
             if(f)break;
             for(auto [b1,b2]:c){
                 ll p=a1*b2+a2*b1;
                 if(p==b){
                     cout<<a1<<' '<<b1<<' '<<a2<<' '<<b2<<'\n';
                     f=true;break;
                 }
             }
         }
         if(!f)cout<<"NO"<<'\n';
     }
     return 0;
 }
 ```

