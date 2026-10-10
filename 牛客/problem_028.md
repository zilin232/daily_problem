- # **题目链接：**

[经此一役小红所向无敌_牛客题霸_牛客网](https://www.nowcoder.com/practice/154f387d84a5491ba7bc28b49c43bb27?channelPut=tracker2)

- # **题目描述：**

经过重重困难，对立和光终于来到魔王城，和最终的大魔王 —— 小红进行决战。 已知小红的血量是 \(10^{999999999}\)。 对立的攻击力是 a，血量是 h。 光的攻击力是 b，血量是 k。

每回合光先对小红发起攻击，然后对立对小红发起攻击，然后小红展开幻术，令光和对立同时互相攻击。 每次攻击后，受击者的血量会减掉攻击者的攻击力。

当光和对立其中一人死亡后，另一人会悲痛欲绝，对小红发出自己攻击力 * 10 的伤害的大招，然后自杀。（若两人同时死亡，则两人都无法发出大招）

小红想知道，弱小的光和对立，她们能对自己造成多少点伤害？

## 输入描述

一行 4 个正整数 \(a,h,b,k\)，用空格隔开。 \(1 \le a,b,h,k \le 10^9\)

## 输出描述

一个正整数，代表小红受到的伤害。

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
     ll a,h,b,k;cin>>a>>h>>b>>k;
     ll k1=(h+b-1)/b,k2=(k+a-1)/a;
     ll ans=(a+b)*min(k1,k2);//至少一人死亡时非大招伤害
     if(k1>k2){
         ans=ans+10*a;
     }else if(k1<k2){
         ans=ans+10*b;
     }
     cout<<ans;
     return 0;
 }
 ```

