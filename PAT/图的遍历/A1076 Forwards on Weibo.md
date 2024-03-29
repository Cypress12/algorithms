Weibo is known as the Chinese version of Twitter. One user on Weibo may have many followers, and may follow many other users as well. Hence a social network is formed with followers relations. When a user makes a post on Weibo, all his/her followers can view and forward his/her post, which can then be forwarded again by their followers. Now given a social network, you are supposed to calculate the maximum potential amount of forwards for any specific user, assuming that only L levels of indirect followers are counted.
### 输入格式
Each input file contains one test case. For each case, the first line contains 2 positive integers: N (≤1000), the number of users; and L (≤6), the number of levels of indirect followers that are counted. Hence it is assumed that all the users are numbered from 1 to N. Then N lines follow, each in the format:
```
M[i] user_list[i]
```
where M[i] (≤100) is the total number of people that user[i] follows; and user_list[i] is a list of the M[i] users that followed by user[i]. It is guaranteed that no one can follow oneself. All the numbers are separated by a space.
Then finally a positive K is given, followed by K UserID's for query.
### 输出格式
For each UserID, you are supposed to print in one line the maximum potential amount of forwards this user can trigger, assuming that everyone who can view the initial post will forward it once, and that only L levels of indirect followers are counted.
### 输入样例
```
7 3
3 2 3 4
0
2 5 6
2 3 1
2 3 4
1 4
1 5
2 2 6
```
### 输出样例
```
4
5
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
vector<int>g[1005];
int n,m,i,j,t,tt,layer[1005];
bool visited[1005];
queue<int> q;
int bfs(int a)
{
    int sum=0,nowlayer=0;
    q.push(a);
    visited[a]= true;
    while (!q.empty()&&nowlayer<m)
    {
        int top = q.front();
        q.pop();
        for (j=0;j<g[top].size();j++)
        {
            if (!visited[g[top][j]])
            {
                layer[g[top][j]] = layer[top]+1;
                if (layer[g[top][j]]>nowlayer)
                    nowlayer = layer[g[top][j]];
                q.push(g[top][j]);
                visited[g[top][j]]= true;
                sum++;
            }
        }
    }
    return sum;
}
int main() {
    cin>>n>>m;
    for (i=1;i<=n;i++)
    {
        cin>>t;
        for (j=0;j<t;j++)
        {
            cin>>tt;
            g[tt].push_back(i);
        }
    }
    cin>>t;
    for (i=0;i<t;i++)
    {
        cin>>tt;
        fill(layer,layer+n+1,0);
        fill(visited,visited+n+1, false);
        cout<<bfs(tt)<<endl;
    }
    return 0;
}
```
