- # **题目链接：**

[Cidoai的植物_牛客题霸_牛客网](https://www.nowcoder.com/practice/a09bcaa6cc384e58b8c90caf49d3462d?channelPut=tracker2)

- # **题目描述：**

# 提取原文

Cidoai 喜欢植物。

Cidoai 有一个 n 行 m 列的花园，这个花园初始没有植物，他会对这个花园做 k 次如下操作之一：

1. 选择第 i 列，在这一列上没有植物的位置上全部种下植物 x；
2. 选择第 a 行第 b 列，如果这个位置有植物，则铲除这株植物，否则不进行操作。

现在它给了你 \(n,m\) 以及它的操作序列，它想知道操作完后花园的状态。 由于输入量过大，操作数列不会被直接输入，而是由参数生成，如下：

```
def rnd():
    p=(1<<32)
    ret=seed
    seed=(seed xor ((seed<<13) mod p)) mod p
    seed=(seed xor ((seed>>17) mod p)) mod p
    seed=(seed xor ((seed<<5) mod p)) mod p
    return ret

for t=1 to k:
    \(op[t]\)=(rnd() mod 2) + 1
    if \(op[t]\)==1:
        i[t]=(rnd() mod m) + 1
        x[t]=(rnd() mod (n*m)) + 1
    if \(op[t]\)==2:
        a[t]=(rnd() mod n) + 1
        b[t]=(rnd() mod m) + 1
```

其中 seed 由输入给定。\(op[t]\) 表示第 t 次操作对应的操作编号，为 1 或 2。若第 t 次操作为 1 操作，\(i[t],x[t]\) 表示对应的列数和植物编号。若第 t 次操作为 2 操作，\(a[t],b[t]\) 表示对应的行数和列数。

rnd 函数的 C++ 代码如下：

```
unsigned seed;
unsigned rnd(){
    unsigned ret=seed;
    seed^=seed<<13;
    seed^=seed>>17;
    seed^=seed<<5;
    return ret;
}
```

由于输出量过大，你不需要输出整个花园的状态，只需要输出如下值即可：

\(\bigoplus_{i=1}^n \bigoplus_{j=1}^m p_{i,j} \times ((i-1)\times m + j)\)

其中 \(p_{i,j}\) 表示花园中第 i 行第 j 列的植物编号，若该位置没有植物，则编号为 0。这个式子表示枚举所有 \(i=1,2,\cdots,n,j=1,2,\cdots,m\)，求得所有 \(p_{i,j}\times((i-1)\times m + j)\) 值后将其异或起来。

## 输入描述

一行四个整数 \(n,m,k,seed\)。 \(1\le n\le 2\times 10^4,1\le m\le 200,1\le k\le 5\times 10^6,0\le seed<2^{32}\)，操作 1 满足 \(1\le i\le m,1\le x\le nm\)，操作 2 满足 \(1\le a\le n,1\le b\le m\)。

## 输出描述

一行一个整数，表示答案。

注意输入和输出的行列顺序。

- # **题目题解：**

 ```cpp
 #include<bits/stdc++.h>
 using namespace std;
 using ll=long long;
 using ull=unsigned long long;
 using ill=__int128;
 const ll mod1=1e9+7;
 const ll mod2=998244353;
 
 unsigned seed;
 unsigned rnd(){
     unsigned ret=seed;
     seed^=seed<<13;
     seed^=seed>>17;
     seed^=seed<<5;
     return ret;
 }
 
 int main(){
     ios::sync_with_stdio(false);
     cin.tie(0);cout.tie(0);
     ll n,m,k;cin>>n>>m>>k>>seed;
     vector<array<ll,3>>qu(k+1);
     for(ll i=1;i<=k;i++){
         ll op=rnd()%2+1;
         ll a=rnd();
         ll b=rnd();
         if(op==1)a%=m,b%=(n*m);
         else a%=n,b%=m;
         a++;b++;
         qu[i]={op,a,b};
     }
 
     vector<vector<ll>>g(n+1,vector<ll>(m+1,0));
     vector<vector<ll>>q(m+1);
     for(ll i=1;i<=n;i++){
         for(ll j=1;j<=m;j++){
             q[j].push_back(i);
         }
     }//第i列的哪几行没有种植物
     for(ll i=1;i<=k;i++){
         auto [po,a1,a2]=qu[i];
         if(po==1){
             while(q[a1].size()){
                 g[q[a1].back()][a1]=a2;
                 q[a1].pop_back();
             }//把ai列没有种植物的地方种上植物。
         }else{
             g[a1][a2]=0;
             q[a2].push_back(a1);
             //除掉这棵植物，将该行加入该列
         }
     }
     ll ans=0;
     for(ll i=1;i<=n;i++){
         for(ll j=1;j<=m;j++){
             ans=ans^(g[i][j]*((i-1)*m+j));
         }
     }//枚举每个位置做对应异或。
     cout<<ans;
     return 0;
 }
 ```

