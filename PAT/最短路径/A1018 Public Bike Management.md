城市里有一些公共自行车站，每个车站的自行车最大容量为一个偶数C<sub>max</sub>，且如果一个车站中自行车数恰好为C<sub>max</sub>/2，那么称该车站处于“完美状态”。而如果一个车站容量是满的或是空的，那么控制中心（PBMC）就会携带或从路上收集一定的自行车前往该车站，使问题车站及沿途所有车站都达到“完美状态”。现在给出C<sub>max</sub>、车站数目N（不含PBMC)、问题车站编号SP、无向边数M及边权，求一条从PBMC（记为0号）到达问题车站SP的最短路径，输出需要从PBMC携带的自行车数目、最短路径、到达问题车站后需要带回的自行车数目。如果最短路径有多条，那么选择从PBMC携带自行车数目最少的；如果仍然有多条，那么选择最后从问题车站带回的自行车数目最少的。注意：沿途所有车站的调整过程必须在前往问题车站的过程中就调整完毕，带回时不再调整。
### 输入格式
Each input file contains one test case. For each case, the first line contains 4 numbers: C<sub>max</sub>(≤100), always an even number, is the maximum capacity of each station; N (≤500), the total number of stations; S<sub>p</sub>, the index of the problem station (the stations are numbered from 1 to N, and PBMC is represented by the vertex 0); and M, the number of roads. The second line contains N non-negative numbers C<sub>i</sub>(i=1,⋯,N) where each C<sub>i</sub> is the current number of bikes at S<sub>i</sub> respectively. Then M lines follow, each contains 3 numbers: S<sub>i</sub>, S<sub>j</sub>, and T<sub>ij</sub> which describe the time T<sub>ij</sub> taken to move betwen stations S<sub>i</sub> and S<sub>j</sub>. All the numbers in a line are separated by a space.
### 输出格式
For each test case, print your results in one line. First output the number of bikes that PBMC must send. Then after one space, output the path in the format: 0−>S<sub>1</sub>−>⋯−>S<sub>p</sub>. Finally after another space, output the number of bikes that we must take back to PBMC after the condition of SP is adjusted to perfect.
Note that if such a path is not unique, output the one that requires minimum number of bikes that we must take back to PBMC. The judge's data guarantee that such a path is unique.
### 输入样例
```
10 3 3 5
6 7 0
0 1 1
0 2 1
0 3 3
1 3 1
2 3 1
```
### 输出样例
```
3 0->2->3 0
```

### 题解
```
#include<iostream>
#include<set>
#include<string>
#include<algorithm>
#include<queue>
#include<vector>
#include<cmath>
using namespace std;
struct node
{
    int v,dis;
};
int cmax,n,sp,m,i,j,d[505],c[505];
vector<node> g[1010];
vector<int> pre[505],path,temppath;
bool vis[505]={false};
void dijkstra(int s)
{
    fill(d,d+n+1,1<<20);
    d[s]=0;
    for (i=0;i<=n;i++)
    {
        int u=-1,min=1<<20;
        for (j=0;j<=n;j++)
        {
            if(vis[j]== false&&d[j]<min)
            {
                u = j;
                min = d[j];
            }
        }
        if (u==-1) return;
        vis[u]= true;
        for (j=0;j<g[u].size();j++)
        {
            int v = g[u][j].v,dis = g[u][j].dis;
            if (d[u]+dis<d[v])
            {
                d[v] = d[u]+dis;
                pre[v].clear();
                pre[v].push_back(u);
            }
            else if (d[u]+dis==d[v])
                pre[v].push_back(u);
        }
    }
}
int back=1<<20,bring=1<<20;
void dfs(int e)
{
    if (e == 0)
    {
        int tempback=0,tempbring=0,now=0;
        for ( i=temppath.size()-1;i>=0;i--)
        {
            if (c[temppath[i]]>0)
            {
                now+=c[temppath[i]];
            }
            else if (c[temppath[i]]<0)
            {
              now+=c[temppath[i]];
              if (now<0)
              {
                  tempbring+=-now;
                  now=0;
              }
            }
        }
       if (now>=0)
       {
           tempback=now;
       }
       if (tempbring<bring)
       {
           bring=tempbring;
           back=tempback;
           path=temppath;
           path.push_back(0);
       }
       else if (tempbring==bring)
       {
           if (tempback<back)
           {
               bring=tempbring;
               back=tempback;
               path=temppath;
               path.push_back(0);
           }
       }
        return;
    }
    temppath.push_back(e);
    for (int ii=0;ii<pre[e].size();ii++)
    {
        dfs(pre[e][ii]);
    }
    temppath.pop_back();
}
int main() {
    cin>>cmax>>n>>sp>>m;
    for (i=1;i<=n;i++)
    {
        cin>>c[i];
        c[i]-=cmax/2;
    }
    for (i=0;i<m;i++)
    {
        node ss,tt;
        int a,b,cc;
        cin>>a>>b>>cc;
        ss.v=a,tt.v=b,ss.dis=tt.dis=cc;
        g[b].push_back(ss);
        g[a].push_back(tt);
    }
    dijkstra(0);
    dfs(sp);
    cout<<bring<<" ";
    for (i=path.size()-1;i>=0;i--)
    {
        cout<<path[i];
        if (i!=0)
            cout<<"->";
    }
    cout<<" "<<back<<endl;
    return 0;
}
```
