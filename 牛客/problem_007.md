- # **题目链接：**

[走一个大整数迷宫_牛客题霸_牛客网](https://www.nowcoder.com/practice/5e28adbc58a443808dead63044a5a079?channelPut=tracker2)

- # **题目描述：**

给定一个 n×m的矩阵迷宫，其中第 i行第 j列的格子权值为

ci,*j*=ai*,*j*×*p^(*2*^bi*,*j)。

LH 起始位于 (1,1)，出口位于 (n,m)。迷宫配有一个**计数器**，初始值为 c1,1。在任意时刻，若计数器的值满足 counter≡0(mod(p−1))，且 LH 身处出口 (n,m)，大门即刻打开，LH 得以逃离。

每经过 1秒，LH 必须向**上、下、左、右**四个方向中的某一方向移动一步（不得停留，也不得走出迷宫）。假设 LH 从 (i,j) 移动到 (i′,j′)，则计数器会累加 ci′,j′。

请计算 LH 最快需要多少秒才能逃离；若无论如何都无法逃离，则输出 −1。

### 输入描述：

输入共三部分：
∙ ∙第一行输入三个整数 n,m,p(1≦n,m≦10; 2≦p≦1e4)；
∙ ∙接下来 n行，每行 m 个整数，构成矩阵 ai,j；
∙ ∙再接下来 n行，每行 m个整数，构成矩阵 bi,j，范围均为 0≦ai,j,bi,j≦1e6。

### 输出描述：

输出一个整数，代表最短逃离时间；若无法逃离，输出 −1。

- # **题目题解：**

因为p^x ![img](file:///C:\Users\刘伟豪\AppData\Local\Temp\ksohtml23828\wps2.jpg) 1(mod p-1),所以![img](file:///C:\Users\刘伟豪\AppData\Local\Temp\ksohtml23828\wps3.jpg) (mod p-1),进而用![img](file:///C:\Users\刘伟豪\AppData\Local\Temp\ksohtml23828\wps4.jpg)%(p-1)来代表![img](file:///C:\Users\刘伟豪\AppData\Local\Temp\ksohtml23828\wps5.jpg)。

定义ti【x】【y】[w]表示到位置x,y且权值和为w的最短时间，初始化为-1，因为这里的最短时间可能是0。

最后我们用BFS广度优先搜索，![img](file:///C:\Users\刘伟豪\AppData\Local\Temp\ksohtml23828\wps6.jpg) =1e6 ,是可以接受的。输出ti【n】【m】【0】即使答案。

 ```cpp
 #include<bits/stdc++.h>
 using namespace std;
 using ll=long long;
 using ull=unsigned long long;
 using ill=__int128;
 const ll mod1=1e9+7;
 const ll mod2=998244353;
 struct d{
     ll x,y,w;
 };
 ll dx[4]={1,0,-1,0};
 ll dy[4]={0,1,0,-1};
 ll ti[11][11][10100];
 int main(){
     ios::sync_with_stdio(false);
     cin.tie(0);cout.tie(0);
     memset(ti,-1,sizeof(ti));
     ll n,m,p;cin>>n>>m>>p;
     vector<vector<ll>>a(n+1,vector<ll>(m+1,0));
     vector<vector<ll>>b(n+1,vector<ll>(m+1,0));
     vector<vector<ll>>c(n+1,vector<ll>(m+1,0));
     for(ll i=1;i<=n;i++)for(ll j=1;j<=m;j++)cin>>a[i][j];
     for(ll i=1;i<=n;i++)for(ll j=1;j<=m;j++)cin>>b[i][j]; 
     for(ll i=1;i<=n;i++){
         for(ll j=1;j<=m;j++){
             c[i][j]=a[i][j]%(p-1);
             //cout<<c[i][j]<<' ';
         }//cout<<'\n';
     }
     queue<d>q;
     q.push({1,1,c[1][1]});
     ti[1][1][c[1][1]]=0;
     //ll ans=-1;
     while(!q.empty()){
         auto it=q.front();q.pop();
         ll x=it.x,y=it.y,w=it.w,t=ti[x][y][w];
         
         for(ll i=0;i<4;i++){
             ll nx=x+dx[i],ny=y+dy[i];
             if(nx>0&&nx<=n&&ny>0&&ny<=m&&ti[nx][ny][(w+c[nx][ny])%(p-1)]==-1){
                 ti[nx][ny][(w+c[nx][ny])%(p-1)]=t+1;
                 q.push({nx,ny,(w+c[nx][ny])%(p-1)});
             }
         }
     }
     //cout<<ans;
     cout<<ti[n][m][0];
     return 0;
 }
 ```

