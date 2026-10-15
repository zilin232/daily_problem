- # **题目链接：**

[F-小月的峰_牛客周赛 Round 165](https://ac.nowcoder.com/acm/contest/141721/F)

- # **题目描述：**

小月要设置一列包含 n 个整数的读数 \(x_1,x_2,\dots,x_n\)。第 i 个读数必须位于给定的闭区间 \([l_i,r_i]\) 中。

这列读数需要先严格上升，再严格下降。也就是说，必须存在一个位置 \(p\ (2 \le p \le n-1)\)，满足：

\(x_1 < x_2 < \dots < x_p > x_{p+1} > \dots > x_n\)

这列读数的步幅是所有相邻读数之差的绝对值的最大值，即：

\(\max_{1\le i<n} |x_{i+1}-x_i|\)

请你帮小月计算在所有合法的读数设置方案中，可能的最小步幅是多少。如果无法设置满足要求的读数，输出 \(-1\)。

## 输入描述

第一行输入一个整数 \(n\ (3 \le n \le 2\times 10^5)\)，表示读数数量。 此后 n 行，第 i 行输入两个整数 \(l_i,r_i\ (-10^9 \le l_i \le r_i \le 10^9)\)，表示第 i 个读数的允许范围。

## 输出描述

如果存在符合要求的读数，输出一个整数，表示步幅的最小可能值；否则，输出 \(-1\)。

- # **题目题解：**

 ```cpp
 #include<bits/stdc++.h>
 using namespace std;
 using ll=long long;
 using ull=unsigned long long;
 using ill=__int128;
 const ll mod1=1e9+7;
 const ll mod2=998244353;
 ll n;
 ll d[200020][2];
 ll fd[200020][2];
 bool ch(ll mid){
     vector<vector<ll>>a(n+1,vector<ll>(2,1e10));
     vector<vector<ll>>b(n+1,vector<ll>(2,1e10+1));
     ll x=d[1][0],s=d[1][1];
     a[1][0]=x;a[1][1]=s;
     for(ll i=2;i<=n;i++){
         x=x+1;s=s+mid;
         x=max(x,d[i][0]);
         s=min(s,d[i][1]);
         if(x>s)break;
         a[i][0]=x;a[i][1]=s;
     }
     x=fd[1][0],s=fd[1][1];
     b[1][0]=x;b[1][1]=s;
     for(ll i=2;i<=n;i++){
         x=x+1;s=s+mid;
         x=max(x,fd[i][0]);
         s=min(s,fd[i][1]);
         if(x>s)break;
         b[i][0]=x;b[i][1]=s;
     }
     for(ll i=1;i<=(n/2);i++)swap(b[i][0],b[n-i+1][0]),swap(b[i][1],b[n-i+1][1]);
     for(ll i=2;i<n;i++){
         if(a[i][0]>b[i][1])continue;
         if(a[i][1]<b[i][0])continue;
         return true;
     }
     return false;
 }
 int main(){
     ios::sync_with_stdio(false);
     cin.tie(0);cout.tie(0);
     cin>>n;
     for(ll i=1;i<=n;i++){
         cin>>d[i][0]>>d[i][1];
         fd[n-i+1][0]=d[i][0];
         fd[n-i+1][1]=d[i][1];
     }
     ll ans=-1;
     ll l=1,r=2e9+10;
     while(l<r){
         ll mid=(l+r)/2;
         if(ch(mid))r=mid,ans=mid;
         else l=mid+1;
     }
     cout<<ans;
     return 0;
 }
 ```

