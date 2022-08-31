As an emergency rescue team leader of a city, you are given a special map of your country. The map shows several scattered cities connected by some roads. Amount of rescue teams in each city and the length of each road between any pair of cities are marked on the map. When there is an emergency call to you from some other city, your job is to lead your men to the place as quickly as possible, and at the mean time, call up as many hands on the way as possible.
### 输入格式
Each input file contains one test case. For each test case, the first line contains 4 positive integers: N (≤500) - the number of cities (and the cities are numbered from 0 to N−1), M - the number of roads, C<sub>1</sub>and C<sub>2</sub>- the cities that you are currently in and that you must save, respectively. The next line contains N integers, where the i-th integer is the number of rescue teams in the i-th city. Then M lines follow, each describes a road with three integers c<sub>1</sub>, c<sub>2</sub>and L, which are the pair of cities connected by a road and the length of that road, respectively. It is guaranteed that there exists at least one path from C<sub>1</sub> to C<sub>2</sub>.
### 输出格式
For each test case, print in one line two numbers: the number of different shortest paths between C<sub>1</sub> and C<sub>2</sub>, and the maximum amount of rescue teams you can possibly gather. All the numbers in a line must be separated by exactly one space, and there is no extra space allowed at the end of a line.
### 输入样例
```
5 6 0 2
1 2 1 5 3
0 1 1
0 2 2
0 3 1
1 2 1
2 4 1
3 4 1
```
### 输出样例
```
2 4
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
int n,m,st,ed,i,d[505],c[505],j;
bool vis[505]={false};
struct node
{
    int v,dis;
};
vector<node> g[505];
vector<int> pre[505],temppath;
void dijkstra(int a)
{
    fill(d,d+n,1<<20);
    d[a]=0;
    for (i=0;i<n;i++)

    {
        int u=-1,zuixiao=1<<20;
        for (j=0;j<n;j++)
        {
            if (vis[j]== false&&d[j]<zuixiao)
            {
                u=j;
                zuixiao=d[j];
            }
        }
        if (u==-1) return;
        vis[u]= true;
        for (j=0;j<g[u].size();j++)
        {
            int v = g[u][j].v,dis = g[u][j].dis;
            if (vis[v]== false)
            {
                if (d[u]+dis<d[v])
                {
                    d[v] =d[u]+dis;
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
int num=0,result=0;
void dfs(int v)
{
    if (v == st)
    {
        num++;
        temppath.push_back(v);
        int value=0;
        for (i=0;i<temppath.size();i++)
        {
            value += c[temppath[i]];
        }
        if (value>result)
            result = value;
        temppath.pop_back();
        return;
    }
    temppath.push_back(v);
    for (int ii=0;ii<pre[v].size();ii++)
        dfs(pre[v][ii]);
    temppath.pop_back();
}
int main() {
    cin>>n>>m>>st>>ed;
    for (i=0;i<n;i++)
        cin>>c[i];
    for (i=0;i<m;i++)
    {
        int s;
        node t,ss;
        cin>>s>>t.v>>t.dis;
        ss.v = s, ss.dis = t.dis;
        g[s].push_back(t);
        g[t.v].push_back(ss);
    }
    dijkstra(st);
    dfs(ed);
    cout<<num<<" "<<result;
    return 0;
}
```
