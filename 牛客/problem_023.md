- # **题目链接：**

[数学考试_牛客题霸_牛客网](https://www.nowcoder.com/practice/62570271633e401bbe25ca9fad32e6d6?channelPut=tracker2)

- # **题目描述：**

牛妹参加了 2022 年普通高校全世界招生统一考试。数学试题太难，她决定复读。 为了在考试中取得更好的成绩，牛妹决定对数学进行特训。特训练习共 n 道题，第 i 题的难度为 \(a_i\)，分值为 \(b_i\)。为了更好提高自己的数学水平，牛妹决定按照题目顺序做题。

做题会对牛妹的压力指数 P 产生影响。牛妹在长期磨练中养成了一颗大心脏，**做完第 i 题后**，牛妹可以选择保持自己的压力指数 P 不变、使 P 增加 \(Q_i\) 或使 P 减少 \(W_i\)。压力指数上限为 K，下限为 0。如果 P 增加 \(Q_i\) 后大于 K，牛妹就不可以选择让自己的压力指数增加 \(Q_i\)；同理，如果 P 减少 \(W_i\) 后小于 0，牛妹就不可以选择让自己的压力指数减少 \(W_i\)。

牛妹相信压力可以转化为动力。当牛妹在压力为 P 的状态下完成第 i 题时，她一定可以做对这一题，并可以积累 \(a_i \times P\) 的经验。但压力太大会反噬牛妹，当 \(P > b_i\) 时，牛妹不能做对第 i 题，无法积累任何经验。请注意，**无论是否做对，都算作完成了第 i 题，在做完后，才更改压力值。**

牛妹想要知道，完成本次数学特训后，她最多可以积累多少经验。牛妹初始的压力值可以由牛妹在 \(0-K\) 范围内自由选定。

请注意，本题的空间限制较为特别，仅有 64MB。

## 输入描述

输入共 \(n+1\) 行。 输入的第一行为两个正整数 \(n,K,\ 1 \le n \le 10^4,1 \le K \le 5\times 10^3\)。 接下来 n 行，每行四个正整数，第 \(i+1\) 行分别为 \(a_i(1 \le a_i \le 10^2),b_i(1 \le b_i \le 10^9),Q_i(1 \le Q_i \le K),W_i(1 \le W_i \le K)\)。

## 输出描述

输出共一行，为牛妹可以积累经验的最大值。

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
     vector<ll>dp(k+1,0);//表示压力值为k时的最大经验
     for(ll i=1;i<=n;i++){
         ll a,b,q,w;cin>>a>>b>>q>>w;
         vector<ll>sw(k+1,-1e15);//完成本轮后的经验
         for(ll j=0;j<=k;j++){
             if(dp[j]==-1e15)continue;
             ll ad= (j<=b)?a*j:0;
             ll v=dp[j]+ad;
             sw[j]=max(sw[j],v);
             if(j+q<=k)sw[j+q]=max(sw[j+q],v);
             if(j-w>=0)sw[j-w]=max(sw[j-w],v);
         }
         dp.swap(sw);
     }
     ll ans=0;
     for(ll i=0;i<=k;i++)ans=max(ans,dp[i]);
     cout<<ans;
     return 0;
 }
 ```

