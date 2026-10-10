- # **题目链接：**

[紫_牛客题霸_牛客网](https://www.nowcoder.com/practice/da67ea3672e8405e9d8f85f0eb22e30a?channelPut=tracker2)

- # **题目描述：**

在古老的魔法图书馆中，两位年轻的魔法学徒小绿和小紫发现了一本记载着神秘二进制魔法的古籍。书中描述了一种通过复制特定咒语来增强魔法威力的方法。她们决定分别研究这个魔法的不同版本：

小绿获得了一段魔法咒语 s，这段咒语仅由字符 0 和 1 组成。她将这段咒语复制 n 次并连接起来，形成新的强化咒语 S。例如，若 \(s = \texttt{"00"}\) 且 \(n=3\)，则 \(S = \texttt{"000000"}\)。

魔法古籍中提到，稳定的魔法序列必须满足单调不减的特性，即序列中不会出现 0 在 1 之后的情况。小绿想知道，这个强化咒语 S 中可以找出多少个不同的**非空子序列**是稳定的魔法序列。由于答案可能很大，请将答案对 \((10^9 + 7)\) 取模后输出。

## 【名词解释】

非空子序列：从原字符串中任意删除字符，且保持剩余字符相对顺序不变所得到的新字符串，至少包含原字符串中的一个字符。即便子序列字符内容相同，像从 `"11"` 不同位置选取得到的 `"1"` 子序列，因选取位置有别，在序列构造意义上也不相同。

## 输入描述

每个测试文件均包含多组测试数据。第一行输入一个整数 \(T\ (1 \le T \le 10^4)\) 代表数据组数，每组测试数据描述如下：

第一行输入一个整数 \(n\ (1 \le n \le 10^{18})\)，表示字符串 s 复制的次数。 第二行输入一个长度不超过 \(10^5\)，仅由字符 `0` 和 `1` 组成的字符串 s，在这个版本中，我们对字符集没有额外的限制。

除此之外，保证单个测试文件中所有输入字符串 s 的长度总和不超过 \(2 \times 10^5\)。

## 输出描述

对于每组测试数据，输出一个整数，表示字符串 S 中单调不减的子序列的数量。由于答案可能非常大，请将结果对 \((10^9 + 7)\) 取模后输出。

- # **题目题解：**

单调不增字串：**全0、左边全0右边全1或全1**

全0、左边全0右边全1：这一类枚举s的每一位0作为该字串的最后一位0
$$
\sum_{i=1}^{n}\sum_{j} 2^{(i-1)*sum_0+pre_0[j]+back_1[j]+(n-i)*sum_1}
=\sum_{i=1}^{n} 2^{(sum_0-sum_1)*i} * \sum_{j} 2^{pre_0[j]+back_1[j]+(n*sum_1-sum_0)}
$$
全1：2^k - 1

 ```cpp
 #include<bits/stdc++.h>
 using namespace std;
 using ll=long long;
 using ull=unsigned long long;
 using ill=__int128;
 const ll mod1=1e9+7;
 const ll mod2=998244353;
 ll m2[200010];
 ll ksm(ll a,ll b){
     ll ans=1;
     a=a%mod1;
     b=b%(mod1-1);
     while(b){
         if(b&1)ans=(ans*a)%mod1;
         a=(a*a)%mod1;
         b=b/2;
     }
     return ans;
 }
 ll ch(ll a,ll b,ll q1,ll q2,ll n){
     ll ans=ksm(2,((((n-1)%(mod1-1))*q2%(mod1-1)+a+b)+mod1-1)%(mod1-1));
     ll p=m2[abs(q1-q2)];
     //cout<<((n-1)%(mod1-1))*q2%(mod1-1)+a+b<<' ';
     //cout<<ans<<' '<<p<<' '<<a<<' '<<b<<' '<<n<<'\n';
     if(q1==q2)return (ans*(n%mod1)+mod1)%mod1;
     if(q1<q2)p=ksm(p,mod1-2);
     ll p1=(ksm(p,n%(mod1-1))-1+mod1)%mod1;
     ll p2=ksm((p-1+mod1)%mod1,mod1-2);
     p=(p1*p2)%mod1;
     ans=(ans*p)%mod1;
     return ans;
 }
 int main(){
     ios::sync_with_stdio(false);
     cin.tie(0);cout.tie(0);
     m2[0]=1;
     for(ll i=1;i<=200000;i++)m2[i]=(m2[i-1]*2)%mod1;
     ll t;cin>>t;
     while(t--){
         ll n;string s;cin>>n>>s;
         ll len=s.size();
         s='/'+s;
         vector<ll>a(len+1,0);
         vector<ll>b(len+2,0);
         for(ll i=1;i<=len;i++){
             a[i]=a[i-1];
             if(s[i]=='0')a[i]++;
         }
         for(ll i=len;i>=1;i--){
             b[i]=b[i+1];
             if(s[i]=='1')b[i]++;
         }
         ll q1=a[len],q2=b[1];
         //cout<<q1<<' '<<q2<<' '<<len<<' '<<n<<'\n';
         ll ans=0;
         for(ll i=1;i<=len;i++){
             if(s[i]=='0'){
                 ans=(ans+ch(a[i-1],b[i+1],q1,q2,n))%mod1;
             }
             //cout<<a[i-1]<<' '<<b[i+1]<<'\n';
             //cout<<ans<<' ';
         }
         ll p=ksm(2,n%(mod1-1)*q2);
         p=(p-1+mod1)%mod1;
         ans=(ans+p)%mod1;
         cout<<ans<<'\n';
     }
     return 0;
 }
 ```

