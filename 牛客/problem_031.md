- # **题目链接：**

[一道难题_牛客题霸_牛客网](https://www.nowcoder.com/practice/ebb82c13f66f492595782a7432357efd?channelPut=tracker2)

- # **题目描述：**

给定一个数字 n，求出 \(1-n\) 中只由 0 或 1 组成的，且至少有三个 1 相连的数（不含前导零）有多少个。

## 输入描述

第一行一个整数 \(n(1 \le n \le 10^{23})\)。

## 输出描述

一个整数，表示满足条件的数的个数。

- # **题目题解：**

解法一：暴力搜索  

\(T(n) =  \boldsymbol{O(n\cdot 2^n)}\)

字符串 `s` 的长度为 n

 ```cpp
 #include<bits/stdc++.h>
 using namespace std;
 using ll=long long;
 using ull=unsigned long long;
 using ill=__int128;
 const ll mod1=1e9+7;
 const ll mod2=998244353;
 string s;
 ll ans;
 void dfs(string p){
     if(p.size()>s.size()||(p.size()==s.size()&&p>s))return;
     if(p.find("111")!=string::npos)ans++;
     dfs(p+'0');
     dfs(p+'1');
 }
 int main(){
     ios::sync_with_stdio(false);
     cin.tie(0);cout.tie(0);
     cin>>s;
     dfs("1");
     cout<<ans;
     return 0;
 }
 ```

解法二：找只有0、1构成的最大 不超过s 的字符串，看成二进制然后枚举1到m（m表示s二进制转十进制的数）

\(T(n) =  \boldsymbol{O(\ 2^n)}\)

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
     string s;
     ll ans=0;
     cin>>s;
     for(ll i=0;i<s.size();i++){
         if(s[i]>'1'){
             s[i]='1';
             for(ll j=i+1;j<s.size();j++)s[j]='1';
             break;
         }
     }
     reverse(s.begin(),s.end());
     ll m=0;
     for(ll i=0;i<s.size();i++){
         if(s[i]=='1')m+=((ll)1<<i);
     }
     for(ll i=1;i<=m;i++){
         if(i&(i>>1)&(i>>2))ans++;
     }
     cout<<ans;
     return 0;
 }
 ```

解法三；数位dp

时间复杂度：L × 3 × 2 × 2 = 12L  ，  L 是输入数字的位数

 ```cpp
 #include<bits/stdc++.h>
 using namespace std;
 #define int long long
 string s;
 // dp[数位位置][末尾连续1数(0~2)][是否自由取值][是否已出现三连1]
 int dp[30][3][2][2];
 // p:当前位 c:末尾连续1数量 f:是否可自由取0/1 ok:是否满足至少三连1
 int dfs(int p,int c,int f,int ok){
 	if(p==s.size())return ok; // 数位遍历完成，返回是否符合条件
 	if(~dp[p][c][f][ok])return dp[p][c][f][ok]; // 记忆化剪枝
 	int res=0,up=f?1:min(s[p]-'0',1); // 当前位枚举上限
 	for(int i=0;i<=up;i++){
 		int nf=f|(i<s[p]-'0'); // 更新自由状态
 		int nc=i?c+1:0; // 更新连续1计数
 		int nok=ok;
 		if(nc>=3)nok=1,nc=0; // 出现三连1，标记满足条件
 		res+=dfs(p+1,nc,nf,nok);
 	}
 	return dp[p][c][f][ok]=res;
 }
 signed main(){
 	cin>>s;
 	memset(dp,-1,sizeof dp); // 初始化记忆化数组
 	cout<<dfs(0,0,0,0);
 }
 
 ```



