- # **题目链接：**

[无关(relationship)_牛客题霸_牛客网](https://www.nowcoder.com/practice/b612f0f9cf1144aea851279dfa2e824b?channelPut=tracker2)

- # **题目描述：**

## 描述

 若一个集合A内所有的元素都**不是**正整数N的因数，则称N与集合A无关。

 给出一个含有k个元素的集合A={a1,a2,a3,...,ak}，求区间[L,R]内与A无关的正整数的个数。

 保证A内的元素都是**素数**。

### 输入描述：

输入数据共两行：

第一行三个正整数L,R,k，意义如“题目描述”。

第二行k个正整数，描述集合A，保证k个正整数两两不相同。

### 输出描述：

输出数据共一行：

第一行一个正整数表示区间[L,R]内与集合A无关的正整数的个数

- # **题目题解：**

两种方法：二进制枚举、递归

二进制枚举：先求有多少数（m）满足 A中至少有一个数是这个数的因数。

通过枚举[1,1<<k)得到A的所有子集，而且根据容斥原理可以判断子集长度 奇加偶减 ，最后区间长度减去m得到答案。

递归：

ch(ll a,ll b)在1到b的正整数中,不被a1[a],a1[a+1], ...,a1[k-1]这几个素数中任何一个整除的数的个数。

 ```cpp
 ll ch(ll a,ll b){
 
 	if(a==k)return b;
 
 	else return ch(a+1,b)-ch(a+1,b/a1[a]);
 //选p - 不选p 
 //每深入一层多一个素数，符号会自动翻转//正好对应奇加偶减
 }
 ```

 ```cpp
 #include<bits/stdc++.h>
 using namespace std;
 using ll=long long;
 using ull=unsigned long long;
 using ill=__int128;
 const ll mod1=1e9+7;
 const ll mod2=998244353;
 ll a1[25];
 ll l,r,k;
 ll ch(ll a,ll b){
     if(a==k)return b;
     else return ch(a+1,b)-ch(a+1,b/a1[a]);
 }
 int main(){
     ios::sync_with_stdio(false);
     cin.tie(0);cout.tie(0);
     //递归
     cin>>l>>r>>k;
     for(ll i=0;i<k;i++)cin>>a1[i];
     cout<<ch(0,r)-ch(0,l-1);
 
 
     //二进制枚举
     //ll l,r,k;cin>>l>>r>>k;
     //vector<ll>a(k,0);
     //for(ll i=0;i<k;i++)cin>>a[i];
     //ll m=1<<k;
     //ll ans=0;
     //for(ll i=1;i<m;i++){
     //    ll p=__builtin_popcountll(i);
     //    ll an=1;
     //    ll q=i;
      //   for(ll j=0;j<k;j++){
      //       if(q&1){
     //            an=an*a[j];
      //       }
      //       q=q/2;
     //        if(an>r)break;
     //    }
     //    if(p&1)ans=ans+(r/an-(l-1)/an);
     //    else ans=ans-(r/an-(l-1)/an);
     //    //cout<<ans<<'\n';
     //}
     //cout<<(r-l+1-ans);
     return 0;
 }
 ```

