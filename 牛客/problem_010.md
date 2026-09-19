- # **题目链接：**

[分割序列_牛客题霸_牛客网](https://www.nowcoder.com/practice/f49a64748c2344c1be65f9be417a495a?channelPut=tracker2)

- # **题目描述：**

给定一个长度为 n 的 01 串 s，你需要把它完全切分成若干连续子串 \(\{t_i\}\)，使得：

1. 对于任意的连续子段 \(t_i\)，命题 “该连续子段 \(t_i\) 内 恰好 包含一个数字字符 1” 恒成立。
2. \(\sum_{i=1}^{|s|} t_i = s\)，即这些切分后的连续子串按切分顺序拼接起来后恰好能得到原字符串 s。

你需要求出满足以上两个要求的切分方案的总数量。由于最终的计算结果可能很大，你只需要输出这个结果对 \((10^9 + 7)\) 取模后的结果即可。

## 输入描述：

在一行上输入一个整数 \(n\ (1 \le n \le 10^5)\)。 在第二行上输入一个长度为 n 的 01 串 \(s\ (s_i \in \{0,1\})\)。

## 输出描述：

输出一个整数，表示满足要求的切分方案数量对 \((10^9 + 7)\) 取模后的结果。

- # **题目题解：**

计算方案数只需将所有  相邻的‘1’间可插入位置数量  相乘即可。

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
     ll n;cin>>n;
     string s;cin>>s;
     ll ans=0;
     ll idx=-1;
     for(ll i=0;i<n;i++){
         if(s[i]=='1'){
             idx=i;
             ans=1;break;
         }
     }
     ll an=1;
     for(ll i=idx+1;i<n;i++){
         if(s[i]=='0')an++;
         else{
             ans=(ans*an)%mod1;
             an=1;
         }
     }
     cout<<ans;
     return 0;
 }
 ```

