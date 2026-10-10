- # **题目链接：**

[区间增量与单点求值_牛客题霸_牛客网](https://www.nowcoder.com/practice/9eafdd79239b4f138a207fe98ee0399d?channelPut=tracker2)

- # **题目描述：**

对于给定的长度为 n 的数组 \(\{a_1,a_2,\dots,a_n\}\)，你需要构建一个能够动态维护区间和信息的数据结构，使得其能支持：

1. 区间增量：将 \([l,r]\) 这个区间中的全部元素修改为其与一个数 x 相加后的值，即 \(\forall i \in [l,r],a_i \to a_i+x\)。
2. 单点求值：输出下标为 x 的元素的值，即 \(a_x\)。

## 输入描述

第一行输入两个整数 \(n,q\ (1 \le n,q \le 10^5)\) 代表数组中的元素数量、操作次数。 第二行输入 n 个整数 \(a_1,a_2,\dots,a_n\ (-10^7 \le a_i \le 10^7)\) 代表初始数组。 此后 q 行，每行先输入一个整数 \(op\ (1 \le op \le 2)\) 代表操作编号，随后：

- 若 \(op=1\)，在同一行输入三个整数 \(l,r,x\ (1 \le l \le r \le n;\ -10^7 \le x \le 10^7)\) 代表区间增量；
- 若 \(op=2\)，在同一行输入一个整数 \(x\ (1 \le x \le n)\) 代表单点求值操作。

## 输出描述

对于每一次询问，输出一行一个整数代表单点求值的结果。保证至少存在一次询问。

- # **题目题解：**

 ```cpp
 #include<bits/stdc++.h>
 using namespace std;
 using ll=long long;
 using ull=unsigned long long;
 using ill=__int128;
 const ll mod1=1e9+7;
 const ll mod2=998244353;
 ll bit[100010];
 ll n;
 void add(ll idx,ll v){
     for(;idx<=n;idx=idx+(idx&-idx)){
         bit[idx]+=v;
     }
 }
 ll qu(ll x){
     ll ans=0;
     for(;x>0;x=x-(x&-x)){
         ans+=bit[x];
     }
     return ans;
 }
 int main(){
     ios::sync_with_stdio(false);
     cin.tie(0);cout.tie(0);
     ll q;cin>>n>>q;
     vector<ll>a(n+1,0);
     for(ll i=1;i<=n;i++){
         cin>>a[i];
         add(i,a[i]-a[i-1]);
     }//将数组转化成差分形式
     while(q--){
         //树状数组区间加减值和单点查询
         ll op;cin>>op;
         if(op==1){
             ll l,r,x;cin>>l>>r>>x;
             add(l,x);
             if(r+1<=n){
                 add(r+1,-x);
             }
         }else{
             ll x;cin>>x;
             cout<<qu(x)<<'\n';
         }
     }
     return 0;
 }
 ```

