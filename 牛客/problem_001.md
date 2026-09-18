- # **题目链接：**

  [「土」秘法地震_牛客题霸_牛客网](https://www.nowcoder.com/practice/c1e6857fa1d343a4a3ce7446e3d39539?channelPut=tracker2)

- # **题目描述：**

帕秋莉掌握了一种土属性魔法 

这种魔法可以在一片k×k大小的一个正方形区域内产生地震

但是如果某片即将产生地震的区域内有建筑物，帕秋莉会停止施法

整个地图大小为n×m，其中一些地方有建筑

请问有多少种可能的情况，使得帕秋莉会停止施法

### 输入描述：

第一行三个数n, m, k，意义见描述
接下来一个n×m的01矩阵表示这篇区域的情况，1表示这个地方有建筑

### 输出描述：

输出一个数表示答案

- # **题目题解：**

首先想到是枚举每一个正方形左上角（x,y),然后对于每一个正方形枚举判断是否有建筑物。  时间复杂度是(n-k+1)*(m-k+1)*k*k ->n^4 超时  

所有想能不能O(1)完成正方形判断降到n^2,

这里我们使用二维前缀和（a[i][j]代表（1，1）到（i，j）这个矩形内的1的数量，a[i][j]=a[i-1][j]+a[i][j-1]-a[i-1][j-1]+d[i][j],d[i][j]代表（i，j）位置是1还是0，是1时d[i][j]是1，是0时d[i][j]是0）获得前缀数量，这样我们就可以用a[i+k-1][j+k-1]-a[i-1][y]-a[x][j-1]+a[i-1][j-1]来获得以（i，j）作为左上角长为k的正方形是否有建筑物，当然二维前缀和的复杂度是n^2,最终该题以 二维前缀和预处理+枚举 来解决问题。

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
     ll n,m,k;cin>>n>>m>>k;
     vector<vector<ll>>a(n+2,vector<ll>(m+2,0));
     for(ll i=1;i<=n;i++){
         string s;cin>>s;
         for(ll j=1;j<=m;j++){
             a[i][j]=s[j-1]-'0';
         }
     }
     for(ll i=1;i<=n;i++){
         for(ll j=1;j<=m;j++){
             a[i][j]=a[i-1][j]+a[i][j-1]-a[i-1][j-1]+a[i][j];
         }
     }
     
     ll ans=0;
     for(ll i=1;i<=n;i++){
         for(ll j=1;j<=m;j++){
             if((j+k-1)>m)break;
             ll x=i+k-1,y=j+k-1;
             if((a[x][y]-a[i-1][y]-a[x][j-1]+a[i-1][j-1])>0){
                 ans++;
             }
         }
         if((i+k-1)>n)break;
     }
     cout<<ans;
     return 0;
 }
 ```

