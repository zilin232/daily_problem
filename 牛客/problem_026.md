- # **题目链接：**

[小红的循环移位_牛客题霸_牛客网](https://www.nowcoder.com/practice/e4cba8d2156844f496c8bb4b5138e532?channelPut=tracker2)

- # **题目描述：**

小红拿到了一个数字串，她每次操作可以使得其向左循环移动一位。 将串 \(s = s_0s_1\dots s_{n-1}\) 向左循环移动一位，将得到串 \(s_1\dots s_{n-1}s_0\)。 小红想知道，使得该数字串变成 4 的倍数，需要最少操作多少次？（可以包含前导零）

## 输入描述

一个数字串，长度不超过 \(10^5\)

## 输出描述

如果无法达成目的，则输出 - 1。 否则输出一个整数，代表最少的操作次数。

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
     string s;cin>>s;
     ll n=s.size();
     ll nn=n;
     ll ans=0;
     ll idx1=n-2,idx2=n-1;
     do{
         if(ans>=nn){
             break;
         }
         ll v=10*(s[idx1]-'0')+(s[idx2]-'0');
         if(v%4==0){
             break;
         }
         //注意
         //s=s+s[ans]的时间复杂度是O(n)，要写成s.push_back(s[ans]);
         idx1=(idx1+1)%n;
         idx2=(idx2+1)%n;
         ans++;
     }while(1);
     if(ans>=nn)ans=-1;
     cout<<ans;
     return 0;
 }
 ```

