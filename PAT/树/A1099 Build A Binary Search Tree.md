二叉树有N个结点，给出每个结点的左右孩子结点的编号（不存在用-1表示）。接着给出一个N个整数的序列，需要把这N个整数填入二叉树的结点中，使得二叉树成为一棵二叉查找树。输出这课二叉树的层序遍历序列。
### 输入格式
Each input file contains one test case. For each case, the first line gives a positive integer N (≤100) which is the total number of nodes in the tree. The next N lines each contains the left and the right children of a node in the format `left_index right_index`, provided that the nodes are numbered from 0 to N−1, and 0 is always the root. If one child is missing, then −1 will represent the NULL child pointer. Finally N distinct integer keys are given in the last line.
### 输出格式
For each test case, print in one line the level order traversal sequence of that tree. All the numbers must be separated by a space, with no extra space at the end of the line.
### 输入样例
```
9
1 6
2 3
-1 -1
-1 4
5 -1
-1 -1
7 -1
-1 8
-1 -1
73 45 11 58 82 25 67 38 42
```
### 输出样例
```
58 25 82 11 38 67 45 73 42
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
    int l;
    int r;
}tree[105];
int n,i,t[105],m=0;
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
    for (i=0;i<n;i++)
    {
        int a,b;
        cin>>a>>b;
        tree[i].l=a;
        tree[i].r=b;
    }
    for (i=0;i<n;i++)
        cin>>t[i];
    sort(t,t+n);
    midorder(0);
    queue<node> q;
    q.push(tree[0]);
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
