- # **题目链接：**

[小跳蛙_牛客题霸_牛客网](https://www.nowcoder.com/practice/46d943dedaee4e9ea7b48d65681296ad?channelPut=tracker2)

- # **题目描述：**

在一个特别长且笔直的小溪的河床上，有 n 块石头露出水面。它们距离小溪源头的距离分别为 \(p_1,p_2,\dots,p_n\)。一只小青蛙正坐在其中一块石头上，准备开始它的跳跃训练。

每次青蛙跳跃到距离它所在石头第 k 近的石头上。具体来说，如果青蛙坐在位置 \(p_i\) 的石头上，那么它将跳到这样的 \(p_j\) 上，使得以下两个条件同时满足：

- \(|\{p_a: |p_a - p_i| < |p_j - p_i|\}| \le k\)
- \(|\{p_a: |p_a - p_i| \le |p_j - p_i|\}| > k\)

特别的，如果 \(p_j\) 不是唯一的，那么青蛙在其中选择距离源头最近的石头。

对于**每一块石头**分别计算，若青蛙从这块石头开始跳跃，经过 m 次跳跃后最终会停留在哪一块石头上？

## 输入描述：

输入的第一行包含三个整数 \(n、k\) 和 m \((1 \le k < n \le 10^6,1 \le m \le 10^{18})\)，用空格分隔，分别表示石头的数量、参数 k 和计划跳跃的次数。

输入的第二行包含 n 个整数 \(p_j\) \((1 \le p_1 < p_2 < \dots < p_n \le 10^{18})\)，用空格分隔，表示小溪河床上连续石头的位置。

## 输出描述：

输出一行 n 个整数 \(r_1,r_2,\dots,r_n\)，用空格分隔。数字 \(r_i\) 表示从输入顺序中的第 i 块石头开始跳跃 m 次后，青蛙最终停留的石头编号。

- # **题目题解：**

 ```cpp
 #include<bits/stdc++.h>
 using namespace std;
 using ll=long long;
 using ull=unsigned long long;
 using ill=__int128;
 const ll mod1=1e9+7;
 const ll mod2=998244353;
 const ll N=1e6+10;
 ll p[N],ans[N],dp[N][2];//初始位置、最终位置、倍增数组（只用到相邻位所以只开2）
 int main(){
     ios::sync_with_stdio(false);
     cin.tie(0);cout.tie(0);
     ll n,k,m;cin>>n>>k>>m;
     for(ll i=1;i<=n;i++)cin>>p[i],ans[i]=i;//初始化
     //滑动窗口，包含i在内的最近的k+1个节点的区间，i位置 移动一次后的位置是区间两端中较大的
     ll l=1,r=l+k;
     for(ll i=1;i<=n;i++){
         while(l<i&r<n&&((p[i]-p[l])>(p[r+1]-p[i]))){
             l++;r++;
         }//对于下一个位置，区间要么不变，要么向右移一位。（如果i超出了区间，区间会自动移到(i,i+k)。
         if((p[i]-p[l])>=(p[r]-p[i]))dp[i][0]=l;
         else dp[i][0]=r;
         if(m&1)ans[i]=dp[i][0];
     }
     
     m>>=1;
     for(ll j=1;m;m>>=1,j^=1){
         for(ll i=1;i<=n;i++){
             dp[i][j]=dp[dp[i][j^1]][j^1];
         }//求倍增，一般情况下dp[i][j]代表i位置移动2**j后的位置，但此处dp只与相邻层有关，且与i-2及其以前的dp是无关，所以可以简化(dp[i][j]=dp[dp[i][j-1]][j-1]-->dp[i][j]=dp[dp[i][j^1]][j^1])
         if(m&1){
             for(ll i=1;i<=n;i++)ans[i]=dp[ans[i]][j];
         }//将m拆成多个2的某次幂相加。
     }
     for(ll i=1;i<=n;i++)cout<<ans[i]<<' ';
     return 0;
 }
 ```

