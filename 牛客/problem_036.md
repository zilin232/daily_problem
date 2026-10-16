- # **题目链接：**

[小红的偶子串_牛客题霸_牛客网](https://www.nowcoder.com/practice/996879349a654069880305671ce3168e?channelPut=tracker2)

- # **题目描述：**

小红定义偶串为：由很多长度为 2 的、两字符相同的字符串拼接而成的字符串。例如：`"aabb"`，`"jjjjkk"`是偶串，而`"aaa"`，`"puup"`则不是偶串。

小红拿到了一个仅由小写字母组成的字符串，她想取一段最长的连续子串为偶串。你能帮小红求出它的长度吗？

## 输入描述

一个仅由小写字母组成的字符串，长度不超过 200000。

## 输出描述

最长的偶子串长度。

> 偶串本质：必须是 `aa + bb + cc + ...` 这种，每两个一组，每组内部字符相等，组与组之间无要求。 也就是字符串必须按每 2 个字符分块，每一块两个字符相同。

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
     ll maxl=0;
     ll a=0;
     ll len=0;
     char c=s[0];
     for(ll i=0;i<n;i++){
         if(s[i]==c)len++;
         else{
             c=s[i];
             a+=(len/2);
             if(len&1){
                 maxl=max(maxl,a);
                 a=len/2;
             }
             len=1;
         }
     }
     a+=(len/2);
     maxl=max(maxl,a);
     cout<<maxl*2;
     return 0;
 }
 ```

