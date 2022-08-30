A graph which is connected and acyclic can be considered a tree. The height of the tree depends on the selected root. Now you are supposed to find the root that results in a highest tree. Such a root is called the deepest root.
### 输入格式
Each input file contains one test case. For each case, the first line contains a positive integer N (≤10<sup>4</sup>) which is the number of nodes, and hence the nodes are numbered from 1 to N. Then N−1 lines follow, each describes an edge by given the two adjacent nodes' numbers.
### 输出格式
For each test case, print each of the deepest roots in a line. If such a root is not unique, print them in increasing order of their numbers. In case that the given graph is not a tree, print `Error: K components` where K is the number of connected components in the graph.
### 输入样例1
```
5
1 2
1 3
1 4
2 5
```
### 输出样例1
```
3
4
5
```
### 输入样例2
```
5
1 3
1 4
2 5
3 4
```
### 输出样例2
```
Error: 2 components
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
vector<int> g[10005];
set<int> re;
bool visited[10005];
int i,n,layer[10005],maxnumlayer=0;
void dfs(int a)
{
    visited[a]=true;
    for (int j=0;j<g[a].size();j++)
    {
        if (!visited[g[a][j]])
            dfs(g[a][j]);
    }
}
int bfs(int a)
{
    queue<int> q;
    q.push(a);
    visited[a]= true;
    int now=0;
    while (!q.empty())
    {
        int top = q.front();
        q.pop();
        for (int j=0;j<g[top].size();j++)
        {
            if (!visited[g[top][j]]) {
                q.push(g[top][j]);
                visited[g[top][j]]= true;
                layer[g[top][j]] = layer[top]+1;
                if (now<layer[g[top][j]])
                    now=layer[g[top][j]];
            }
        }
    }
    return now;
}
int main() {
    cin>>n;
    for (i=0;i<n-1;i++)
    {
        int a,b;
        cin>>a>>b;
        g[a].push_back(b);
        g[b].push_back(a);
    }
    fill(visited, visited+n+1, false);
    int block=0;
    for (i=1;i<=n;i++)
    {
        if (!visited[i])
        {
            dfs(i);
            block++;
        }
    }
    if (block>1)
        cout<<"Error: "<<block<<" components"<<endl;
    else
    {
        for (i=1;i<=n;i++)
        {
            fill(visited,visited+n+1, false);
            fill(layer,layer+n+1,0);
            int numlayer = bfs(i);
            if (numlayer>maxnumlayer)
            {
                re.clear();
                re.insert(i);
                maxnumlayer = numlayer;
            }
            else if (numlayer==maxnumlayer)
                re.insert(i);
        }
        for (set<int>::iterator it=re.begin();it!=re.end();it++)
            cout<<*it<<endl;
    }
    return 0;
}
```
