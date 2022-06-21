给出二叉树每个结点的左右孩子结点的编号，把二叉树反转，输出反转后二叉树的层序遍历序列和中序遍历序列
### 输入格式
Each input file contains one test case. For each case, the first line gives a positive integer N (≤10) which is the total number of nodes in the tree -- and hence the nodes are numbered from 0 to N−1. Then N lines follow, each corresponds to a node from 0 to N−1, and gives the indices of the left and right children of the node. If the child does not exist, a - will be put at the position. Any pair of children are separated by a space.
### 输出格式
For each test case, print in the first line the level-order, and then in the second line the in-order traversal sequences of the inverted tree. There must be exactly one space between any adjacent numbers, and no extra space at the end of the line.
### 输入样例
```
8
1 -
- -
0 -
2 7
- -
- -
5 -
4 6
```
### 输出样例
```
3 7 2 6 4 0 5 1
6 5 7 4 3 2 0 1
```

### 题解
```
#include<iostream>
#include<stack>
#include<string>
#include<cstring>
#include<queue>
 using namespace std;
 struct  node
 {
    int child[2];
 }tree[15];
bool root[15];
int s=0,n;
void levelorder(int root)
{
    queue<int>q;
    q.push(root);
    while(!q.empty())
    {
        cout<<q.front();
        if (s!=n-1)
            cout<<" ";
        for (int ii=1;ii>=0;ii--)
        {
            if(tree[q.front()].child[ii]!=-1)
                q.push(tree[q.front()].child[ii]);
        }
        s++;
        q.pop();
    }
    cout<<endl;
}
void inorder(int i)
{
    if (i==-1)
        return;
    inorder(tree[i].child[1]);
    cout<<i;
    if (s!=n-1)
    {
        cout<<" ";
        s++;
    }
    inorder(tree[i].child[0]);
}
 int main()
 {
     memset(root,1,sizeof(root));
     int i,j;
     cin>>n;
     for (i=0;i<n;i++)
     {
         for (j=0;j<2;j++)
         {
            char c;
            cin>>c;
            if (c!='-')
            {
                int num=c-'0';
                tree[i].child[j]=num;
                root[num]=false;
            }
            else
                tree[i].child[j]=-1;
         }
     }
     for (i=0;i<n;i++)
     {
         if (root[i])
            break;
     }
     levelorder(i);
     s=0;
     inorder(i);
 }
```
