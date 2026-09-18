~~~c++
# 题目：土秘法地震
题目链接：https://ac.nowcoder.com/acm/problem/15145

## 题目描述
帕秋莉掌握了一种土属性魔法
这种魔法可以在一片k×k大小的一个正方形区域内产生地震
但是如果某片即将产生地震的区域内有建筑物，帕秋莉会停止施法
整个地图大小为n×m，其中一些地方有建筑
请问有多少种可能的情况，使得帕秋莉会停止施法

**输入描述**
第一行三个数n, m, k，意义见描述
接下来一个n×m的01矩阵表示这篇区域的情况，1表示这个地方有建筑

**输出描述**
输出一个数表示答案

## 题解
暴力思路：枚举每一个正方形左上角 $(x,y)$，然后逐个格子判断是否有建筑物。
时间复杂度：$(n-k+1)\times(m-k+1)\times k\times k \rightarrow O(n^4)$，会超时。

优化方案：**二维前缀和**
$a[i][j]$ 代表 $(1,1)$ 到 $(i,j)$ 这个矩形内1的数量。
二维前缀和公式：
$$a[i][j]=a[i-1][j]+a[i][j-1]-a[i-1][j-1]+d[i][j]$$
$d[i][j]$ 代表 $(i,j)$ 位置是1还是0。

查询以 $(i,j)$ 为左上角、边长为 $k$ 的正方形内建筑总数：
$$sum = a[i+k-1][j+k-1]-a[i-1][j+k-1]-a[i+k-1][j-1]+a[i-1][j-1]$$
$sum>0$ 代表正方形内存在建筑，答案+1。
预处理$O(nm)$，枚举$O(nm)$，总复杂度 $O(nm)$。

## C++ 代码
```cpp
#include<bits/stdc++.h>
using namespace std;
using ll=long long;
using ull=unsigned long long;
using i128=__int128;
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
    //二维前缀和预处理
    for(ll i=1;i<=n;i++){
        for(ll j=1;j<=m;j++){
            a[i][j]=a[i-1][j]+a[i][j-1]-a[i-1][j-1]+a[i][j];
        }
    }
    ll ans=0;
    for(ll i=1;i<=n;i++){
        if((i+k-1)>n)break;
        for(ll j=1;j<=m;j++){
            if((j+k-1)>m)break;
            ll x=i+k-1,y=j+k-1;
            if((a[x][y]-a[i-1][y]-a[x][j-1]+a[i-1][j-1])>0){
                ans++;
            }
        }
    }
    cout<<ans;
    return 0;
}
~~~
