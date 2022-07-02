A family hierarchy is usually presented by a pedigree tree where all the nodes on the same level belong to the same generation. Your task is to find the generation with the largest population.
### 输入格式
Each input file contains one test case. Each case starts with two positive integers N (<100) which is the total number of family members in the tree (and hence assume that all the members are numbered from 01 to N), and M (<N) which is the number of family members who have children. Then M lines follow, each contains the information of a family member in the following format:
```
ID K ID[1] ID[2] ... ID[K]
```
where ID is a two-digit number representing a family member, K (>0) is the number of his/her children, followed by a sequence of two-digit ID's of his/her children. For the sake of simplicity, let us fix the root ID to be 01. All the numbers in a line are separated by a space.
### 输出格式
For each test case, print in one line the largest population number and the level of the corresponding generation. It is assumed that such a generation is unique, and the root level is defined to be 1.
### 输入样例
```
23 13
21 1 23
01 4 03 02 04 05
03 3 06 07 08
06 2 12 13
13 1 21
08 2 15 16
02 2 09 10
11 2 19 20
17 1 22
05 1 11
07 1 14
09 1 17
10 1 18
```
### 输出样例
```
9 4
```

### 题解
```
#include<iostream>
#include<stack>
#include<string>
#include<cstring>
#include<queue>
#include<vector>
#include<cmath>
 using namespace std;
 struct node
 {
     int layer;
     double price;
     vector<int>child;
 }tree[100005];
  bool flag[100005];
 int n,i,j,m,num[100005];
 vector<int>::iterator it;

 int main()
 {
    memset(flag,1,sizeof(flag));
    cin>>n>>m;
    for (i=0;i<m;i++)
    {
        int k,l;
        cin>>k>>l;
        for (j=0;j<l;j++)
        {
            int t;
            cin>>t;
            flag[t]=false;
            tree[k].child.push_back(t);
        }
    }
    for (i=1; i<=n; i++)
    {
        if (flag[i])
            break;
    }
    queue<node>q;
    tree[i].layer=1;
    q.push(tree[i]);
    while(!q.empty())
    {
        node top = q.front();
        q.pop();
        num[top.layer]++;
        if (top.child.size())
        {
            for (it=top.child.begin();it!=top.child.end();it++)
            {
                tree[*it].layer = top.layer+1;
                q.push(tree[*it]);
            }
        }
    }
    int sum=0,xiabiao;
    for (i=1;i<=n;i++)
    {
        if (num[i]>sum)
        {
            sum=num[i];
            xiabiao = i;
        }
    }
    printf("%d %d",sum,xiabiao);
    return 0;
 }
```
