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
             //这里内部可以用二分来写。
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

另外一种解法

**p 是合数：核心循环** 

从小到大枚举 `i`（即候选的 n），每次执行以下操作：

- 如果 `i` 和当前 `p` 不互质（有公共因子）：
  1. 把 `p` 除以 `gcd(i,p)`—— 相当于把 p 中所有 `i` 的素因子都去掉，模拟「\(i!\) 贡献了这些因子」。
  2. 如果 `p == 1`：说明 \(i!\) 已经覆盖了原 p 的所有素因子，输出 `i` 并结束循环。
  3. 如果 `i < p` 且剩余的 `p` 是素数：说明剩下的最后一个素因子只能由等于它本身的数提供，因此最小 n 就是这个剩余素数，直接输出并提前终止循环。

 ```cpp
 #include<bits/stdc++.h>
 using namespace std;
 using ll=long long;
 using ull=unsigned long long;
 using ill=__int128;
 const ll mod1=1e9+7;
 const ll mod2=998244353;
 bool is(int n){
     if(n==1)  return false;
     for(int i=2;i*i<=n;i++){
         if(n%i==0)  return false;
     }
     return true;
 }//判断是不是质数
 int main(){
     int t;
     cin>>t;
     while(t--){
         int p;
         cin>>p;
         if(p==1)  cout<<p<<endl;
         else if(is(p))  cout<<p<<endl;  //素数
         else{   //不是素数
             for(int i=2;;i++){
                 if(gcd(i,p)!=1){
                     p/=gcd(i,p);
                     if(p==1){
                         cout<<i<<endl;
                         break;
                     }
                     if(i<p&&isprimer(p)){
                         cout<<p<<endl;
                         break;
                     }
                 }
             }
         }
     }
     return 0;
 }
 ```

