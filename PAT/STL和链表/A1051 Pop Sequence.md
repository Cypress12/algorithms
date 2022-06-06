Given a stack which can keep M numbers at most. Push N numbers in the order of 1, 2, 3, ..., N and pop randomly. You are supposed to tell if a given sequence of numbers is a possible pop sequence of the stack. For example, if M is 5 and N is 7, we can obtain 1, 2, 3, 4, 5, 6, 7 from the stack, but not 3, 2, 1, 7, 5, 6, 4.
### 输入格式
Each input file contains one test case. For each case, the first line contains 3 numbers (all no more than 1000): M (the maximum capacity of the stack), N (the length of push sequence), and K (the number of pop sequences to be checked). Then K lines follow, each contains a pop sequence of N numbers. All the numbers in a line are separated by a space.
### 输出格式
For each pop sequence, print in one line "YES" if it is indeed a possible pop sequence of the stack, or "NO" if not.
### 输入样例
```
5 7 5
1 2 3 4 5 6 7
3 2 1 7 5 6 4
7 6 5 4 3 2 1
5 6 4 3 7 2 1
1 7 6 5 4 3 2
```
### 输出样例
```
YES
NO
NO
YES
NO
```

### 题解
```
#include <iostream>
#include <vector>
#include <string>
#include <cstring>
#include <cstdio>
#include <cmath>
#include <algorithm>
#include <map>
#include <stack>
using namespace std;

int b[1005],c[1005];
int main()
{
    int m,n,k,i,j,top=1,le=0;
    bool flag;
    cin>>m>>n>>k;
    for (i=1;i<=1000;i++)
        b[i]=i;
    for (i=0; i<k; i++)
    {
        top=1;
        le=1;
        flag=true;
        stack<int>a;
        for (j=0; j<n; j++)
          cin>>c[j];
        for (j=0; j<n; j++)
        {
            while ((a.empty()||a.top()!=c[j])&&le<=m)
            {
                a.push(b[top]);
                top++;
                le++;
            }
            if (a.top()==c[j])
            {
                a.pop();
                le--;
            }
            else
            {
                flag=false;
                break;
            }
        }
        if(flag)
            cout<<"YES"<<endl;
        else
            cout<<"NO"<<endl;
    }
    return 0;
}
```
