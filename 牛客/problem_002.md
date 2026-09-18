- # **题目链接：**

[走廊的灯_牛客题霸_牛客网](https://www.nowcoder.com/practice/c4986923605c4050986050eb8bfe29ac?channelPut=tracker2)

- # **题目描述：**

走廊里一共有一排共 n盏灯，其中有的灯是灭的，用 0 表示，有的灯是亮的，用 1 表示，还有的灯是闪烁的，用 2 表示。

最长有多少盏连续的灯不包含亮着的灯或不包含灭了的灯（满足任意一个即可）？

### 输入描述：

第一行一个整数 T*T* 表示数据组数。T≤100。

接下来每组数据中第一行一个整数 n，第二行一个长度为 n的字符串 s表示灯的明灭。1≤n,∑n≤1e5，si∈{0,1,2}。

### 输出描述：

对于每组数据输出一行一个整数表示答案。

- # **题目题解：**

对于这题先看简易版，只有0和1，这样我们只需要判断最大相同连续的1或者0即可。记作x函数

在这题2可以看作0或1，那么对于...002222111...这种一般形式来说，把全部的2都看成0或者都看成1是最优的，因为假设现在是002221122举例，换成001111111是最好的，如果哪怕换成0001111111，最长会减一。但我们也不知道

都换成1好还是0好，那么我们就可以把换成1和换成0都做一次x函数，取最大值。  

时间复杂度是 ![img](file:///C:\Users\刘伟豪\AppData\Local\Temp\ksohtml23828\wps1.jpg) ，|s|指s字符串的长度

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
         ll n;string s;cin>>n>>s;
         ll maxl=0;
         char c=s[0];
         ll m=0;
         for(ll i=0;i<n;i++){
             
         }
         maxl=max(maxl,m);
         cout<<maxl<<'\n';
     }
     return 0;
 }
 ```

