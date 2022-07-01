给出一棵销售供应的树，树根唯一。在树根处货物的价格为P，然后从结点开始每往子节点走一层，该层的货物价格将会在父亲结点的价格上增加r%。给出每个叶节点的货物量，求它们的价格之和。
### 输入格式
Each input file contains one test case. For each case, the first line contains three positive numbers: N (≤10 
<sup>5</sup>), the total number of the members in the supply chain (and hence their ID's are numbered from 0 to N−1, and the root supplier's ID is 0); P, the unit price given by the root supplier; and r, the percentage rate of price increment for each distributor or retailer. Then N lines follow, each describes a distributor or retailer in the following format:\
`K<sub>i</sub>ID[1] ID[2] ... ID[K<sub>i</sub>]`\
where in the i-th line, K<sup>i</sup>is the total number of distributors or retailers who receive products from supplier i, and is then followed by the ID's of these distributors or retailers. K<sub>j</sub>being 0 means that the j-th member is a retailer, then instead the total amount of the product will be given after K<sub>j</sub>. All the numbers in a line are separated by a space.
### 输出格式
For each test case, print in one line the total sales we can expect from all the retailers, accurate up to 1 decimal place. It is guaranteed that the number will not exceed 10<sup>10</sup>.
### 输入样例
```
10 1.80 1.00
3 2 3 5
1 9
1 4
1 7
0 7
2 6 1
1 8
0 9
0 4
0 3
```
### 输出样例
```
42.4
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
     int price;
     vector<int>child;
 }tree[100005];
 int n,i,j;
 double p,r;
 bool flag[100005];
 vector<int>::iterator it;
 int main()
 {
     memset(flag,1,sizeof(flag));
    cin>>n>>p>>r;
    r/=100;
    for (i=0;i<n;i++)
    {
        int m;
        cin>>m;
        if (m)
        {
            for(j=0; j<m; j++)
            {
                int t;
                cin>>t;
                flag[t]=false;
                tree[i].child.push_back(t);
            }
        }
        else
        {
            cin>>tree[i].price;
        }
    }
    for (i=0; i<n; i++)
    {
        if (flag[i])
            break;
    }
    double sum=0;
    queue<node>q;
    tree[i].layer=0;
    q.push(tree[i]);
    while(!q.empty())
    {
        node top = q.front();
        q.pop();
        if (top.child.size())
        {
            for (it=top.child.begin();it!=top.child.end();it++)
            {
                tree[*it].layer = top.layer+1;
                q.push(tree[*it]);
            }
        }
        else
        {
            sum += top.price * pow(1+r,top.layer);
        }
    }
    printf("%.1lf",sum*p);
    return 0;
 }
```
