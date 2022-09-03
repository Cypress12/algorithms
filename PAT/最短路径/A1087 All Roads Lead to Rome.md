Indeed there are many different tourist routes from our city to Rome. You are supposed to find your clients the route with the least cost while gaining the most happiness.
### 输入格式
Each input file contains one test case. For each case, the first line contains 2 positive integers N (2≤N≤200), the number of cities, and K, the total number of routes between pairs of cities; followed by the name of the starting city. The next N−1 lines each gives the name of a city and an integer that represents the happiness one can gain from that city, except the starting city. Then K lines follow, each describes a route between two cities in the format `City1 City2 Cost`. Here the name of a city is a string of 3 capital English letters, and the destination is always `ROM` which represents Rome.
### 输出格式
For each test case, we are supposed to find the route with the least cost. If such a route is not unique, the one with the maximum happiness will be recommanded. If such a route is still not unique, then we output the one with the maximum average happiness -- it is guaranteed by the judge that such a solution exists and is unique.
Hence in the first line of output, you must print 4 numbers: the number of different routes with the least cost, the cost, the happiness, and the average happiness (take the integer part only) of the recommanded route. Then in the next line, you are supposed to print the route in the format `City1->City2->...->ROM`.
### 输入样例
```
6 7 HZH
ROM 100
PKN 40
GDN 55
PRS 95
BLN 80
ROM GDN 1
BLN ROM 1
HZH PKN 1
PRS ROM 2
BLN HZH 2
PKN GDN 1
HZH PRS 1
```
### 输出样例
```
3 3 195 97
HZH->PRS->ROM
```

### 题解
```
#include<iostream>
#include<set>
#include<string>
#include<algorithm>
#include<queue>
#include<vector>
#include "map"
#include<cmath>
using namespace std;
struct node
{
    int v,dis;
};
int n,m,i,j,c[205],d[205];
map<string,int> c2n;
map<int,string> n2c;
vector<node> g[205];
vector<int> pre[205],temppath,path;
bool vis[205]={false};
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
                u=j;
                min=d[j];
            }
        }
        if (u==-1) return;
        vis[u]= true;
        for (j=0;j<g[u].size();j++)
        {
            int v=g[u][j].v,dis = g[u][j].dis;
            if (d[u]+dis<d[v])
            {
                d[v] = d[u] +dis;
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
int num=0,totalweight=0,aveweight=0;
void dfs(int e)
{
    if (e==0)
    {
        num++;
        int tempweight=0,tempaveweight=0;
        for (i=0;i<temppath.size();i++)
            tempweight+=c[temppath[i]];
        tempaveweight = tempweight/temppath.size();
        if (tempweight>totalweight)
        {
            totalweight = tempweight;
            aveweight = tempaveweight;
            path = temppath;
            path.push_back(e);
        }
        else if (tempweight == totalweight)
        {
            if (tempaveweight>aveweight)
            {
                aveweight = tempaveweight;
                path = temppath;
                path.push_back(e);
            }
        }
        return;
    }
    temppath.push_back(e);
    for (int ii=0;ii<pre[e].size();ii++)
        dfs(pre[e][ii]);
    temppath.pop_back();
}
int main() {
    cin>>n>>m;
    int t;
    string city;
    cin>>city;
    c2n[city]=0;
    n2c[0] = city;
    for (i=1;i<n;i++)
    {
        cin>>city>>c[i];
        c2n[city]=i;
        n2c[i]=city;
    }
    for (i=0;i<m;i++)
    {
        node ss,tt;
        string city1,city2;
        cin>>city1>>city2>>t;
        ss.dis=tt.dis=t;
        ss.v=c2n[city1];
        tt.v=c2n[city2];
        g[c2n[city2]].push_back(ss);
        g[c2n[city1]].push_back(tt);
    }
    dijkstra(0);
    dfs(c2n["ROM"]);
    cout<<num<<" "<<d[c2n["ROM"]]<<" "<<totalweight<<" "<<aveweight<<endl;
    for (i=path.size()-1;i>=0;i--)
    {
        cout<<n2c[path[i]];
        if (i!=0)
            cout<<"->";
    }
    return 0;
}
```
