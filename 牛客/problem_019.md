- # **题目链接：**

[阶乘_牛客题霸_牛客网](https://www.nowcoder.com/practice/f44bc1d564f747e291f639bce91a06f9?channelPut=tracker2)

- # **题目描述：**

给定一个正整数 p 求一个最小的正整数 n，使得 n! 是 p 的倍数

输入描述: 第一行输入一个正整数 T 表示测试数据组数 接下来 T 行，每行一个正整数 p

输出描述: 输出 T 行，对于每组测试数据输出满足条件的最小的 n

- # **题目题解：**

 ```cpp
 #include<bits/stdc++.h>
 using namespace std;
 using ll=long long;
 using ull=unsigned long long;
 using ill=__int128;
 const ll mod1=1e9+7;
 const ll mod2=998244353;
 ll to(ll a,ll b){
     ll ans=0;
     while(a){
         ans=ans+a/b;
         a=a/b;
     }
     return ans;
 }// a的阶乘 包含多少个质因子b
 int main(){
     ios::sync_with_stdio(false);
     cin.tie(0);cout.tie(0);
     int t;cin>>t;
     while(t--){
         ll p;cin>>p;
         if(p==1){cout<<1<<'\n';continue;}
         vector<ll>d;
         vector<ll>nm;
         for(ll i=2;i*i<=p;i++){
             if(p%i==0){
                 d.push_back(i);
                 ll an=0;
                 while(p%i==0){
                     p=p/i;
                     an++;
                 }
                 nm.push_back(an);
             }
         }//分解质因数
         if(p!=1){
             d.push_back(p);
             nm.push_back(1);
         }//放入超大质数
         ll q=0;
         ll n=d.size();
         for(ll i=0;i<n;i++){
             ll an=0;
             while(to(an,d[i])<nm[i]){
                 an+=d[i];
             }//容纳d[i]**nm[i]的最小数
             q=max(q,an);
             //取这些最小数的最大
         }
         cout<<q<<'\n';
     }
     return 0;
 }
 ```

