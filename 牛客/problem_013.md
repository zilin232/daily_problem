- # **题目链接：**

[数树_牛客题霸_牛客网](https://www.nowcoder.com/practice/3b7340fc6d914e18a2a0784680542d14?channelPut=tracker2)

- # **题目描述：**

“开导！”

众所周知，树是一种特殊的图。

众所周知（二），导出子图是由该图顶点的一个子集和该图中两端均在该子集的所有边的集合组成的图。

注 1：二叉树是有向图。

注 2：有向图的导出子图，还是有向图。

小沙有 n 个节点，他需要你构造出一颗有根二叉树，使得二叉树的所有导出子图是一颗满二叉树的数目尽可能多。

请问构造出来的有根二叉树的所有导出子图是一颗满二叉树的数目最多是多少？

你能帮帮不会数 / 树的小沙吗？

## 输入描述：

第一行读入一个整数 T，代表多组样例。

随后 T 行，每行输入一个正整数 n。

保证有 \(1 \le T \le 10^5,\ 1 \le n \le 10^{18}\)。

## 输出描述：

对于每组样例输出一行整数代表答案。

由于答案过大，所以请输出答案对 \(10^9 + 7\) 取模的值。

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
     ll a[62]={0};a[1]=1;//i层满二叉树的子图为满二叉树的数量
     for(ll i=2;i<=61;i++){
         ll p=((ll)1)<<(i-1);
         p=p%mod1;
         a[i]=(a[i-1]+p*2-1)%mod1;
     }//每多加一层，该层节点与之前的节点的每一个节点都可以作为根构建一个满二叉树
     int t;cin>>t;
     while(t--){
         ll n;cin>>n;
         ll m=n;
         ll p=1;
         ll an=0;
         while(p<=n){
             p=p*2+1;
             an++;
             if((p)>n)break;
         }//计算能放满几层
         ll ans=a[an]%mod1;
         n=n-((p-1)/2);
         for(ll i=1;i<=an;i++){
             if(n&1){
                 ans=(ans+(((ll)1)<<i)%mod1-1)%mod1;
             }
             n=n/2;
         }
         //将剩余节点分成多个二的某次幂相加
         //对于每一个2的某次幂（记作2的i次幂）都可以看作往一个i层高的满二叉树新加一层。
         cout<<(ans+mod1)%mod1<<'\n';
     }
     return 0;
 }
 ```

