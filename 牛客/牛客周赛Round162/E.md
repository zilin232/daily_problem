- # **题目链接：**

[E-小月的区间_牛客周赛 Round 162](https://ac.nowcoder.com/acm/contest/140489/E)

- # **题目描述：**

小月有一个长度为 n 的排列 \(a = a_1,a_2,\dots,a_n\)。

她称一个非空子数组 \([l,r]\) 是**新鲜的**，当且仅当它同时满足以下两个条件：

- 数组中的最大值，大于所有位于数组左侧的元素，即大于每个 \(a_i\ (i < l)\)；
- 数组中的最小值，小于所有位于数组右侧的元素，即小于每个 \(a_i\ (i > r)\)。

请你统计新鲜子数组的数量。

【名词解释】 长度为 n 的排列：由 \(1,2,\dots,n\) 这 n 个整数、按任意顺序组成的数组（每个整数均恰好出现一次）。例如，\(\{2,3,1,5,4\}\) 是一个长度为 5 的排列，而 \(\{1,2,2\}\) 和 \(\{1,3,4\}\) 都不是排列，因为前者存在重复元素，后者包含了超出范围的数。

子数组：从原数组中，连续选择一段元素（可以全选，不可以不选）得到的新数组。由原数组的第 l 个元素到第 r 个元素组成的子数组可以用 \([l,r]\) 表示。

## 输入描述

第一行输入一个整数 \(n\ (1 \le n \le 2 \times 10^5)\)。 第二行输入 n 个整数 \(a_1,a_2,\dots,a_n\ (1 \le a_i \le n)\)。

## 输出描述

输出一个整数，代表新鲜子数组的数量。

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
     int n;cin>>n;
     vector<int>a(n);
     for(int i=0;i<n;i++)cin>>a[i];
     vector<int>p;int cmax=-1;//从前到后出现更大值的下标
     for(int i=0;i<n;i++)if(a[i]>cmax)cmax=a[i],p.push_back(i);
     vector<int>q;int cmin=n+1;//从后到前出现更小值的下标
     for(int i=n-1;i>=0;i--)if(a[i]<cmin)cmin=a[i],q.push_back(i);
     reverse(q.begin(),q.end());
     ll ans=0;
     //一个满足条件的区间必然包含至少 一个p值下标和一个q值下标
     //否则区间左测（右侧）数据至少有一个数比区间最大（最小）更大（更小）
     for(int r=0;r<n;r++){//枚举右边界
         int k=upper_bound(p.begin(),p.end(),r)-p.begin()-1;
         int maxl=p[k];//第一个小于r的p的下标 
         int m=upper_bound(q.begin(),q.end(),r)-q.begin()-1;
         int qr=(m>=0)?q[m]:-1;//第一个小于r的q的下标
         int rr=min(qr,r);
         if(rr<0)continue;
         ans+=min(maxl,rr)+1;
     }
     cout<<ans<<'\n';
     return 0;
 }
 
 ```

