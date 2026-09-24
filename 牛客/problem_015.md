- # **题目链接：**

[Calling_牛客题霸_牛客网](https://www.nowcoder.com/practice/d6e7ae7f1d604e6e8e68fcf72f7dac29?channelPut=tracker2)

- # **题目描述：**

你有 6 种正方形纸片，其中第 \(i(1 \le i \le 6)\) 种边长为 i，每一种都有 \(k_i\) 个，你需要把它们放在**至多 s 个面积为 \(36(=6\times6)\) 的正方形框中**，显然我们可以一个框一个框的放，要求如下：

每个框不必放满。比如你可以把至多 36 个边长为 1 的正方形纸片放在一个框中，也可以把 30 个边长为 1 的正方形放在一个框中，也可以把 1 个边长为 5 的正方形纸片放在一个框中，等。 每个框放的正方形边长不必相同。比如一个框中可以同时出现边长为 3 和边长为 1 的正方形。

请问能否放得下，若可以，输出 Yes，否则输出 No。

## 输入描述：

第一行，一个正整数 \(T(1 \le T \le 10^5)\)，表示 T 组数据。

对于每组数据： 第一行，一个非负整数 \(s(0 \le s \le 10^9)\)。 第二行，6 个非负整数，为 \(k_i(0 \le k_i \le 10^4)\)。

## 输出描述：

T 行，每行一个字符串 Yes 或 No，表示对应数据的答案。

请注意区分大小写。

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
     int t;cin>>t;
     while(t--){
         //从大到小的用正方形填充。
         ll s;
         ll k[7]={0};
         cin>>s;
         for(ll i=1;i<=6;i++)cin>>k[i];
         s-=k[6];//用6X6的填充
         s-=k[5];k[1]=max((ll)0,k[1]-k[5]*11);
         //用5x5填充，然后用1x1的填充缝隙
         s-=k[4];
         if(k[2]>=(k[4]*5))k[2]=k[2]-k[4]*5;
         else{
             ll z=(k[4]*5-k[2])*4;
             k[2]=0;
             k[1]-=min(k[1],z);
         }
         //用4x4填充，然后用2x2填充，2x2不够用1x1填充
         s-=(k[3]/4);k[3]=k[3]%4;
         if(k[3]>0){
             s--;
             if(k[3]==1){
                 ll z1=min((ll)5,k[2]);
                 k[2]-=z1;
                 ll q=27-z1*4;
                 ll z2=min(q,k[1]);
                 k[1]-=z2;
             }else if(k[3]==2){
                 ll z1=min((ll)3,k[2]);
                 k[2]-=z1;
                 ll q=18-z1*4;
                 ll z2=min(q,k[1]);
                 k[1]-=z2;
             }else if(k[3]==3){
                 ll z1=min((ll)1,k[2]);
                 k[2]-=z1;
                 ll q=9-z1*4;
                 ll z2=min(q,k[1]);
                 k[1]-=z2;
             }
         }
         //用3x3填充，然后用2x2填充，2x2不够用1x1填充
         s-=(k[2]/9);k[2]=k[2]%9;
         if(k[2]>0){
             s--;
             ll q=(ll)36-k[2]*4;
             k[1]-=min(k[1],q);
         }
         //用2x2填充，然后用1x1填充
         s-=(k[1]/36);k[1]=k[1]%36;
         if(k[1]>0)s--;
         //用1x1填充，多余的放到一起。
         if(s>=0)cout<<"Yes"<<'\n';
         else cout<<"No"<<'\n';
     }
     return 0;
 }
 ```

