- # **题目链接：**

[多项式输出_牛客题霸_牛客网](https://www.nowcoder.com/practice/142ee43d3e7345d385328faca9f636e5?channelPut=tracker2)

- # **题目描述：**

给定一元 n 次多项式

\(f(x)=a_nx^n + a_{n-1}x^{n-1} + \dots + a_1x + a_0,\) 其中 \(a_n \neq 0\)，系数 \(a_i\ (0 \le i \le n)\) 满足 \(-100 \le a_i \le 100\)。

请按如下规则将多项式输出为字符串：

- 从高次到低次依次输出；
- 系数为 0 的项完全省略；
- 对于次数大于等于 1 的项，若其系数为 1 或 \(-1\)，则省略系数的绝对值 1（常数项即使为 1 或 \(-1\) 也应完整输出）；
- 次数为 0 仅输出常数；次数为 1 输出 x；次数 \(\ge 2\) 输出 \(\boldsymbol{x^\wedge k}\)；
- 输出的第一个非零项（即最高次项）若系数为正，不输出前导加号；后续正系数项前需加 `+`，负系数项加 `-`。

# 输入描述：

第一行输入整数 \(n\ (1 \le n \le 100)\)，表示多项式次数。 第二行输入 \(n + 1\) 个整数 \(a_n,a_{n-1},\dots,a_0\)，依次为 n 次项到 0 次项（常数项）的系数。

# 输出描述：

在一行输出格式化后的多项式字符串。

- # **题目题解：**

 ```cpp
 #include<bits/stdc++.h>
 using namespace std;
 using ll=long long; 
 //分成三部分，前n-2、n-1、n
 void Solve(){
     int n , a , f = 1 ;
     cin >> n ;     
     n++;
     while(n > 2){
         cin >> a ;
         n--;
         if(a==0)continue ;
          
         if(f){
             if(a==1){
                 cout << "x^" << n ;
             }else if(a==-1){
                 cout << "-x^" << n ;
             }else if(a > 0){
                 cout << a << "x^" << n ;
             }else if(a < 0){
                 cout << a << "x^" << n ;
             }
             f = 0 ;
         }else{
             if(a==1){
                 cout << "+x^" << n ;
             }else if(a==-1){
                 cout << "-x^" << n ;
             }else if(a > 0){
                 cout << "+" << a << "x^" << n ;
             }else if(a < 0){
                 cout << a << "x^" << n ;
             }
         } 
     } 
     cin >> a ;
     if(a && f){
         if(a==1){
             cout << "x" ;
         }else if(a==-1){
             cout << "-x" ;
         }else if(a > 0){
             cout << a << "x" ;
         }else if(a < 0){
             cout << a << "x" ;
         }
         f = 0 ;
     }else{
         if(a==1){
             cout << "+x" ;
         }else if(a==-1){
             cout << "-x" ;
         }else if(a > 0){
             cout << "+" << a << "x" ;
         }else if(a < 0){
             cout << a << "x" ;
         }
     }
     cin >> a ;
     if(f){
         cout << a ;
         f = 0 ;
     }else{
         if(a > 0){
             cout << "+" << a ;
         }else if(a < 0){
             cout << a ;
         }
     }
 }
 int main(){
     int T = 1 ;
     while(T--)Solve();
     return 0 ;
 }
 ```

