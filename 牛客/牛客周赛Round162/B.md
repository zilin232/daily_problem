- # **题目链接：**

[B-小月的周长_牛客周赛 Round 162](https://ac.nowcoder.com/acm/contest/140489/B)

- # **题目描述：**

# 题目描述

小月有一张由 \(n \times m\) 个单位正方形纸片按照 n 行 m 列摆放得到的长方形纸。单位正方形纸片的边长为 1。 现在她将第 x 行和第 y 列的所有正方形纸片移除。剩余未被移除的正方形纸片保持原位，请计算这些剩余正方形纸片组成图形的周长之和。

## 输入描述

每个测试文件均包含多组测试数据。第一行输入一个整数 \(T\ (1 \le T \le 10^3)\) 代表数据组数，每组测试数据描述如下： 第一行输入四个整数 \(n,m,x,y\ (1 \le n,m \le 50;\ 1 \le x \le n;\ 1 \le y \le m)\)，表示纸的行数、列数、取走的行、列。 除此之外，保证单个测试文件的 \(n \times m\) 之和不超过 \(2 \times 10^5\)。

## 输出描述

对于每一组测试数据，新起一行。输出一个整数，表示剩余纸片的周长之和。

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
     //分四种情况：在角上、在边上、在内部、只有一个
     int t;cin>>t;
     while(t--){
         ll n,m,x,y;cin>>n>>m>>x>>y;
         if(n==1||m==1)cout<<0<<'\n';
         else if((x==1&&y==1)||(x==1&&y==m)||(x==n&&y==1)||(x==n&&y==m)){
             cout<<(2*n+2*m-4)<<'\n';
         }else if(x==1||x==n){
             cout<<(2*m-4+4*n-2)<<'\n';
         }else if(y==1||y==m){
             cout<<(2*n-2+4*m-4)<<'\n';
         }
         else cout<<(4*m+4*n-8)<<'\n';
     }
     return 0;
 }
 ```

