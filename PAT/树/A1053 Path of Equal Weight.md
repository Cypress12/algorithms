给出树的结构和权值，找从根结点到叶子结点的路径上的权值相加之和等于给定目标数的路径，并且从大到小输出路径。
### 输入格式
Each input file contains one test case. Each case starts with a line containing 0<N≤100, the number of nodes in a tree, M (<N), the number of non-leaf nodes, and 0<S<2<sup>30</sup>, the given weight number. The next line contains N positive numbers where W<sub>i</sub>(<1000) corresponds to the tree node T<sub>i</sub>. Then M lines follow, each in the format:
```
ID K ID[1] ID[2] ... ID[K]
```
where ID is a two-digit number representing a given non-leaf node, K is the number of its children, followed by a sequence of two-digit ID's of its children. For the sake of simplicity, let us fix the root ID to be 00.
### 输出格式
For each test case, print all the paths with weight S in non-increasing order. Each path occupies a line with printed weights from the root to the leaf in order. All the numbers must be separated by a space with no extra space at the end of the line.
### 输入样例
```
20 9 24
10 2 4 3 5 10 2 18 9 7 2 2 1 3 12 1 8 6 2 2
00 4 01 02 03 04
02 1 05
04 2 06 07
03 3 11 12 13
06 1 09
07 2 08 10
16 1 15
13 3 14 16 17
17 2 18 19
```
### 输出样例
```
10 5 2 7
10 4 10
10 3 3 6 2
10 3 3 6 2
```

### 题解
```
//必须把得到的路径保存下来再排序，输入时按照结点权值从大到小排序并且边遍历路径边输出的方法会导致最后一个测试点答案错误
#include <cstdio>
#include <cstring>
#include <algorithm>
#include <queue>
#include <iostream>
#include <vector>
using namespace std;
int n,m,i,j,num[105],path[105],s,p=0;
struct node
{
    int weight;
    vector<int> child;
}tree[105];
vector<int>result[105];
bool cmp(vector<int> a,vector<int>b)
{
    for (int t=0;t<min(a.size(),b.size());t++)
    {
        if (a[t]!=b[t])
            return a[t]>b[t];
    }
    return false;
}
void dfs(int index,int numnode,int sum)
{
    if (sum>s) return;
    if(sum==s)
    {
        if (tree[index].child.size())
            return;
        for (i=0;i<numnode;i++)
        {
            result[p].push_back(tree[path[i]].weight);
        }
        p++;
        return;
    }
    for (int ii=0;ii<tree[index].child.size();ii++)
    {
        int child = tree[index].child[ii];
        path[numnode]=child;
        dfs(child, numnode+1, sum+tree[child].weight);
    }
}
int main()
{
    scanf("%d %d %d",&n,&m,&s);
    for (i=0;i<n;i++)
    {
        scanf("%d",&tree[i].weight);
    }
    for (i=0;i<m;i++)
    {
        int a,b;
        scanf("%d %d",&a,&b);
        for (j=0;j<b;j++)
        {
            int tt;
            cin>>tt;
            tree[a].child.push_back(tt);

        }
    }
    path[0]=0;
    dfs(0,1,tree[0].weight);
    sort(result,result+p,cmp);
    for (i=0;i<p;i++)
    {
        for (j=0;j<result[i].size();j++)
        {
            cout<<result[i][j];
            if (j!=result[i].size()-1)
                cout<<" ";
        }
        cout<<endl;
    }
    return 0;
}
```
