A traveler's map gives the distances between cities along the highways, together with the cost of each highway. Now you are supposed to write a program to help a traveler to decide the shortest path between his/her starting city and the destination. If such a shortest path is not unique, you are supposed to output the one with the minimum cost, which is guaranteed to be unique.
### 输入格式
Each input file contains one test case. Each case starts with a line containing 4 positive integers N, M, S, and D, where N (≤500) is the number of cities (and hence the cities are numbered from 0 to N−1); M is the number of highways; S and D are the starting and the destination cities, respectively. Then M lines follow, each provides the information of a highway, in the format:
```
City1 City2 Distance Cost
```
where the numbers are all integers no more than 500, and are separated by a space.
### 输出格式
For each test case, print in one line the cities along the shortest path from the starting point to the destination, followed by the total distance and the total cost of the path. The numbers must be separated by a space and there must be no extra space at the end of output.
### 输入样例
```
4 5 0 3
0 1 1 20
1 3 2 30
0 3 4 10
0 2 2 20
2 3 1 20
```
### 输出样例
```
0 2 3 3 40
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
    int v,dis,cost;
};
int n,m,s,e,d[505],i,j;
vector<node> g[505];
vector<int> pre[505],temppath,path;
bool vis[505]={false};
void dijkstra(int s)
{
    fill(d,d+n,1<<20);
    d[s]=0;
    for (i=0;i<n;i++)
    {
        int u=-1,min=1<<20;
        for (j=0;j<n;j++)
        {
            if (vis[j]== false&&d[j]<min)
            {
                min=d[j];
                u=j;
            }
        }
        if (u==-1) return;
        vis[u]= true;
        for (j=0;j<g[u].size();j++)
        {
            int v=g[u][j].v,dis = g[u][j].dis;
            if (vis[v]== false)
            {
                if (d[u]+dis<d[v])
                {
                    d[v]=d[u]+dis;
                    pre[v].clear();
                    pre[v].push_back(u);
                }
                else if (d[u]+dis==d[v])
                {
                    pre[v].push_back(u);
                }
            }
        }
    }
}
int cost=1<<20;
void dfs(int ee)
{
    if (s==ee)
    {
        temppath.push_back(ee);
        int tempcost=0;
        for (i=0;i<temppath.size()-1;i++)
        {
            for (j=0;j<g[temppath[i]].size();j++)
            {
                if (g[temppath[i]][j].v==temppath[i+1])
                {
                    tempcost+=g[temppath[i]][j].cost;
                    break;
                }
            }
        }
        if (tempcost<cost)
        {
            cost = tempcost;
            path = temppath;
        }
        temppath.pop_back();
        return;
    }
    temppath.push_back(ee);
    for (int ii=0;ii<pre[ee].size();ii++)
        dfs(pre[ee][ii]);
    temppath.pop_back();
}
int main() {
    cin>>n>>m>>s>>e;
    for (i=0;i<m;i++)
    {
        node ss,tt;
        int a,b,f,k;
        cin>>a>>b>>f>>k;
        ss.dis=tt.dis=f;
        ss.cost=tt.cost=k;
        ss.v=a;
        tt.v=b;
        g[b].push_back(ss);
        g[a].push_back(tt);
    }
    dijkstra(s);
    dfs(e);
    for (i=path.size()-1;i>=0;i--)
    {
        cout<<path[i]<<" ";
    }
    cout<<d[e]<<" "<<cost<<endl;
    return 0;
}
```
