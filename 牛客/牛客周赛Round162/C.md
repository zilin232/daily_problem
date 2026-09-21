- # **题目链接：**

[C-小月的数码轮_牛客周赛 Round 162](https://ac.nowcoder.com/acm/contest/140489/C)

- # **题目描述：**

# 题目描述

小月把 n 个数码轮排成一行，每个数码轮显示一个十进制数字。初始时数码轮显示的数字用一个长为 n 的字符串 \(s = s_1s_2\dots s_n\) 表示，其中 \(s_n\) 表示个位，\(s_{n-1}\) 表示十位，以此类推。

每按一次按钮，所有数码轮都会向前转动一格：0 变成 1，1 变成 2，依此类推，9 变成 0。

小月准备选择一个整数 \(x\ (0 \le x \le 9)\)，使得按 x 次按钮后，数码轮表示的十进制整数被给定的整数 m 整除。请统计有多少种可选择的 x。

读出的数字串允许包含前导零。例如，"008" 表示整数 8，"000" 表示整数 0。整数 0 能被任意正整数整除。

## 输入描述

第一行输入两个整数 \(n,m\ (1 \le n \le 2 \times 10^5;\ 1 \le m \le 10^9)\)，分别表示数码轮数量、除数。 第二行输入一个长度为 n、仅由十进制数字构成的字符串 s，表示初始读数。

## 输出描述

输出一个整数，表示满足要求的按钮次数 x 的数量。

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
     ll n,m;cin>>n>>m;
     string s;cin>>s;
     ll ans=0;
     //枚举每一个x判断是否成立
     for(ll x=0;x<10;x++){
         ll an=0;
         for(ll i=0;i<n;i++){
             ll p=((s[i]-'0')+x)%10;
             an=(an*10%m+p)%m;
         }
         if(an%m==0)ans++;
     }
     cout<<ans;
     return 0;
 }
 ```

