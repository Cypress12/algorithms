A family hierarchy is usually presented by a pedigree tree. Your job is to count those family members who have no child.
### 输入格式
Each input file contains one test case. Each case starts with a line containing 0<N<100, the number of nodes in a tree, and M (<N), the number of non-leaf nodes. Then M lines follow, each in the format:
```
ID K ID[1] ID[2] ... ID[K]
```
where ID is a two-digit number representing a given non-leaf node, K is the number of its children, followed by a sequence of two-digit ID's of its children. For the sake of simplicity, let us fix the root ID to be 01.
The input ends with N being 0. That case must NOT be processed.
### 输出格式
For each test case, you are supposed to count those family members who have no child for every seniority level starting from the root. The numbers must be printed in a line, separated by a space, and there must be no extra space at the end of each line.
The sample case represents a tree with only 2 nodes, where 01 is the root and 02 is its only child. Hence on the root 01 level, there is 0 leaf node; and on the next level, there is 1 leaf node. Then we should output 0 1 in a line.
### 输入样例
```
2 1
01 1 02
```
### 输出样例
```
0 1
```

### 题解
```
#include <cstdio>
#include <cstring>
#include <algorithm>
#include <queue>
#include <iostream>
#include <vector>
using namespace std;
int n,m,i,j,num[105],maxlayer=0;
bool flag[105];
struct node
{
    int layer;
    vector<int> child;
}tree[105];
int main()
{
    cin>>n>>m;
    fill(flag,flag+n,true);
    for (i=0;i<m;i++)
    {
        int a,b;
        cin>>a>>b;
        for (j=0;j<b;j++)
        {
            int tt;
            cin>>tt;
            tree[a].child.push_back(tt);
            flag[tt]=true;
        }
    }
    for (i=1;i<=n;i++)
    {
        if (flag[i])
            break;
    }
    tree[i].layer=0;
    queue<node>q;
    q.push(tree[i]);
    while(!q.empty())
    {
        node top = q.front();
        q.pop();
        if (top.child.size())
        {
            for (i=0;i<top.child.size();i++)
            {
                tree[top.child[i]].layer=top.layer+1;
                q.push(tree[top.child[i]]);
            }
        }
        else
            num[top.layer]++;
        maxlayer = max(maxlayer,top.layer);
    }
    for (i=0;i<=maxlayer;i++)
    {
        cout<<num[i];
        if (i!=maxlayer)
            cout<<" ";
    }
    return 0;
}
```
