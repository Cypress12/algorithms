给出N个非负整数，要用它们构建一棵完全二叉排序树。输出这棵完全二叉排序树的层序遍历序列。
### 输入格式
Each input file contains one test case. For each case, the first line contains a positive integer N (≤1000). Then N distinct non-negative integer keys are given in the next line. All the numbers in a line are separated by a space and are no greater than 2000.
### 输出格式
For each test case, print in one line the level order traversal sequence of the corresponding complete binary search tree. All the numbers in a line must be separated by a space, and there must be no extra space at the end of the line.
### 输入样例
```
10
1 2 3 4 5 6 7 8 9 0
```
### 输出样例
```
6 3 8 1 5 7 9 0 2 4
```

### 题解
```
#include<iostream>
#include<stack>
#include<string>
#include<algorithm>
#include<queue>
#include<vector>
#include<cmath>
 using namespace std;
struct node
{
    int data;
    int l=-1;
    int r=-1;
}tree[1005];
int n,i,t[1005],m=0;
void midorder(int root)
{
    if (root==-1)
        return;
    midorder(tree[root].l);
    tree[root].data = t[m++];
    midorder(tree[root].r);
}
 int main()
 {
    cin>>n;
    for (i=1;i<=n;i++)
    {
        if (i*2<=n)
            tree[i].l=i*2;
        else
            tree[i].l=-1;
        if (i*2+1<=n)
            tree[i].r=i*2+1;
        else
            tree[i].r=-1;
    }
    for (i=0;i<n;i++)
        cin>>t[i];
    sort(t,t+n);
    midorder(1);
    queue<node> q;
    q.push(tree[1]);
    m=0;
    while(!q.empty())
    {
        node top = q.front();
        cout<<top.data;
        m++;
        if (m!=n)
            cout<<" ";
        q.pop();
        if (top.l!=-1)
            q.push(tree[top.l]);
        if (top.r!=-1)
            q.push(tree[top.r]);
    }
    return 0;
 }
```
