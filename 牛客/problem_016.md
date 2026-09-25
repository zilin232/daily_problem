- # **题目链接：**

[三角形取数(Hard Version)_牛客题霸_牛客网](https://www.nowcoder.com/practice/ceea5825472940dabfec917ef93538e6?channelPut=tracker2)

- # **题目描述：**

给定一个由 n 行构成的数字三角形。第 i 行共有 \(2i-1\) 个整数，整体形状如下图所示（以 \(n=3\) 为例）：

```
        1
      2 3 4
    5 6 7 8 9
```

从顶点（第一行唯一的数字）出发，依次向下移动恰好 \(n-1\) 次直到抵达最后一行。 假设当前位于第 i 行第 j 列：

1. 可以向正下方移动至第 \((i+1)\) 行第 j 列；
2. 可以向左下方移动至第 \((i+1)\) 行第 \((j-1)\) 列；
3. 可以向右下方移动至第 \((i+1)\) 行第 \((j+1)\) 列。

每到达一个位置都会获得该位置的数值。定义在整个行走过程中，向左下方移动的次数记为 l，向右下方移动的次数记为 r。 我们需要满足

\(|l-r| \le k\)

请你选择一条合法路径，使得获得数值之和最大，并输出该最大值。

# 输入描述：

在一行上输入两个整数 \(n,k\ (1 \le n \le 300;\ 0 \le k \le n)\)，分别表示数字三角形的行数与允许的移动差。 此后 n 行，第 i 行输入 \(2i-1\) 个整数 \(a_{i,1},a_{i,2},\dots,a_{i,2i-1}\ (-2\times10^9 \le a_{i,j} \le 2\times10^9)\)

共计 \(\sum_{i=1}^{n}(2i-1)=n^2\) 个整数。

# 输出描述：

输出一个整数，表示满足条件的路径可以取得的最大数值之和。

- # **题目题解：**

这里有一个需要稍微注意的点：是最终位置的(l-r)<=k，不是过程中的位置。

除此之外就是一个正常的dp

 ```cpp
 #include<bits/stdc++.h>
 using namespace std;
 using ll=long long;
 using ull=unsigned long long;
 using ill=__int128;
 const ll mod1=1e9+7;
 const ll mod2=998244353;
 ll dy[3]={-1,0,1};
 ll dx[3]={1,1,1};
 //该位置能走的方向
 int main(){
     ios::sync_with_stdio(false);
     cin.tie(0);cout.tie(0);
     ll n,k;cin>>n>>k;
     vector<vector<ll>>a(n+1,vector<ll>(2*n+1,-2e15));
     for(ll i=1;i<=n;i++){
         for(ll j=(n-i+1);j<=(n+i-1);j++){
             cin>>a[i][j];
         }
     }
     //输入n*(2n-1)的形式
     vector<vector<ll>>ans(n+1,vector<ll>(2*n+1,-2e15));
     ans[1][n]=a[1][n];
     for(ll i=1;i<n;i++){
         for(ll j=(n-i+1);j<=(n+i-1);j++){
             for(ll k=0;k<3;k++){
                 ll px=i+dx[k];
                 ll py=j+dy[k];
                 ans[px][py]=max(ans[i][j]+a[px][py],ans[px][py]);
                 //走到这个位置的最大值。
             }
         }
     }
     ll maxl=-2e15;
     for(ll i=(n-k);i<=(n+k);i++){
         maxl=max(maxl,ans[n][i]);
     }
     cout<<maxl;
     return 0;
 }
 ```

