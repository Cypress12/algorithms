给出树的前序（push）和中序（pop）序列，求后序序列
### 输入格式
Each input file contains one test case. For each case, the first line contains a positive integer N (≤30) which is the total number of nodes in a tree (and hence the nodes are numbered from 1 to N). Then 2N lines follow, each describes a stack operation in the format: "Push X" where X is the index of the node being pushed onto the stack; or "Pop" meaning to pop one node from the stack.
### 输出格式
For each test case, print the postorder traversal sequence of the corresponding tree in one line. A solution is guaranteed to exist. All the numbers must be separated by exactly one space, and there must be no extra space at the end of the line.
### 输入样例
```
6
Push 1
Push 2
Push 3
Pop
Pop
Push 4
Pop
Pop
Push 5
Push 6
Pop
Pop
```
### 输出样例
```
3 4 2 6 5 1
```

### 题解
```
#include <cstdio>
#include <cstring>
#include <algorithm>
#include <stack>
#include <iostream>
#include <string>
using namespace std;

const int maxn = 40;

int n;
int pre[maxn], in[maxn], post[maxn];
stack<int> st;
struct node
{
    int data;
    node* lchild, *rchild;
};

node* create(int preL, int preR, int inL, int inR)
{
    if (preL > preR)
        return 0;
    node* root = new node;
    root -> data = pre[preL];
    int k;
    for (k = inL; k < inR; k ++)
    {
        if (in[k] == pre[preL])
            break;
    }
    int numLeft = k - inL;
    root -> lchild = create(preL + 1, preL + numLeft, inL, k - 1);
    root -> rchild = create(preL + numLeft + 1, preR, k + 1, inR);
    return root;
}

int num = 0;
void postOrder(node* root)
{
    if (root == NULL)
        return;
    postOrder(root -> lchild);
    postOrder(root -> rchild);

    printf("%d", root -> data);
    num ++;
    if (num < n)
        printf(" ");
}


int main()
{
    scanf("%d", &n);
    string str;
    int x, preIndex = 0, inIndex = 0;
    for (int i = 0; i < 2 * n; i ++)
    {
        cin>>str;
        if (str== "Push")
        {
            scanf("%d", &x);
            pre[preIndex ++] = x;
            st.push(x);
        }
        else
        {
            in[inIndex ++] = st.top();
            st.pop();
        }
    }
    node* root = create(0, n - 1, 0, n - 1);
    postOrder(root);

    return 0;
}
```
