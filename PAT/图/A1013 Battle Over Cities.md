It is vitally important to have all the cities connected by highways in a war. If a city is occupied by the enemy, all the highways from/toward that city are closed. We must know immediately if we need to repair any other highways to keep the rest of the cities connected. Given the map of cities which have all the remaining highways marked, you are supposed to tell the number of highways need to be repaired, quickly.
For example, if we have 3 cities and 2 highways connecting city 
1
​	
 -city 
2
​	
  and city 
1
​	
 -city 
3
​	
 . Then if city 
1
​	
  is occupied by the enemy, we must have 1 highway repaired, that is the highway city 
2
​	
 -city 
3
​	
 .
### 输入格式
Each input file contains one test case. Each case starts with a line containing 3 numbers N (<1000), M and K, which are the total number of cities, the number of remaining highways, and the number of cities to be checked, respectively. Then M lines follow, each describes a highway by 2 integers, which are the numbers of the cities the highway connects. The cities are numbered from 1 to N. Finally there is a line containing K numbers, which represent the cities we concern.
### 输出格式
For each of the K cities, output in a line the number of highways need to be repaired if that city is lost.
### 输入样例
```
3 2 3
1 2
1 3
1 2 3
```
### 输出样例
```
1
0
0
```

### 题解
```
#include <iostream>
#include <cstring>
#include <vector>
#include <cstdio>
using namespace std;
const int N=5000;
vector<int> g[N];
bool vis[N];
int cp;
void dfs(int v)
{
    if (v==cp) return;
    vis[v]=true;
    for (int i=0;i<g[v].size();i++)
    {
        if (vis[g[v][i]]==false)
            dfs(g[v][i]);
    }
}
int m,n,k;
int main()
{
  cin>>n>>m>>k;
  for (int i=0;i<m;i++)
  {
      int a,b;
      cin>>a>>b;
      g[a].push_back(b);
      g[b].push_back(a);
  }
  for (int q=0;q<k;q++)
  {
      cin>>cp;
      memset(vis,false,sizeof(vis));
      int block=0;
      for (int i=1;i<=n;i++)
      {
          if (i!=cp&&vis[i]==false)
          {
              dfs(i);
              block++;
          }
      }
      cout<<block-1<<endl;
  }
    return 0;
}
```
