给出一棵销售供应的树，树根唯一。在树根处货物的价格为P，然后从结点开始每往子节点走一层，该层的货物价格将会在父亲结点的价格上增加r%。求所有叶结点中的最高价格以及这个价格的叶结点个数
### 输入格式
Each input file contains one test case. For each case, the first line contains three positive numbers: N (≤10 
<sup>5</sup>), the total number of the members in the supply chain (and hence their ID's are numbered from 0 to N−1, and the root supplier's ID is 0); P, the unit price given by the root supplier; and r, the percentage rate of price increment for each distributor or retailer. 
Then the next line contains N numbers, each number S<sub>i</sub> is the index of the supplier for the i-th member. S<sub>root</sub> for the root supplier is defined to be −1. All the numbers in a line are separated by a space.
### 输出格式
For each test case, print in one line the highest price we can expect from some retailers, accurate up to 2 decimal places, and the number of retailers that sell at the highest price. There must be one space between the two numbers.  It is guaranteed that the number will not exceed 10<sup>10</sup>.
### 输入样例
```
9 1.80 1.00
1 5 4 4 -1 4 5 3 6
```
### 输出样例
```
1.85 2
```

### 题解
```
#A1079基础上改的，非最优解
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
 int n,i,j,root;
 double p,r,da=-1;
 vector<int>::iterator it;
 vector<node> leaf;
 int main()
 {
    cin>>n>>p>>r;
    r/=100;
    for (i=0;i<n;i++)
    {
        int m;
        cin>>m;
        if (m!=-1)
        {
            tree[m].child.push_back(i);
        }
        else
            root=i;
    }
    queue<node>q;
    tree[root].layer=0;
    q.push(tree[root]);
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
            top.price= p * pow(1+r,top.layer);
            if (top.price>da)
                da=top.price;
            leaf.push_back(top);
        }
    }
    int sum=0;
    for (i=0;i<leaf.size();i++)
    {
        if (leaf[i].price==da)
            sum++;
    }
    printf("%.2lf %d",da,sum);
    return 0;
 }
```
