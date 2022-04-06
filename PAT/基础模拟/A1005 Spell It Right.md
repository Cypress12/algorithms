Given a non-negative integer N, your task is to compute the sum of all the digits of N, and output every digit of the sum in English.
### 输入格式
Each input file contains one test case. Each case occupies one line which contains an N (≤10<sup>100</sup>).
### 输出格式
For each test case, output in one line the digits of the sum in English words. There must be one space between two consecutive words, but no extra space at the end of a line.
### 输入样例
```
12345
```
### 输出样例
```
one five
```

### 题解
```
#极大数用string
#include <iostream>
#include <algorithm>
#include <string>
#include <cstdio>
using namespace std;
char num[10][10]={"zero","one","two","three","four","five","six","seven","eight","nine"};
string ans[100005],n;
int main()
{
    int sum=0,i=0,j;
    cin>>n;
    for (j=0;j<n.length();j++)
    {
        sum += (n[j]-'0')%10;
    }
    do
    {
        ans[i++] += num[sum%10];
        sum/=10;
    }while(sum>0);
    for (i=i-1;i>=0;i--)
    {
        cout<<ans[i];
        if (i!=0) cout<<" ";
    }
    return 0;
}

```
