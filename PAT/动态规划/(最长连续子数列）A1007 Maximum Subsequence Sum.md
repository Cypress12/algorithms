Given a sequence of K integers { N<sub>1</sub>, N<sub>2</sub>, ..., N<sub>K</sub>}. A continuous subsequence is defined to be { N<sub>i</sub>, N<sub>i+1</sub>, ..., N<sub>j</sub>} where 1≤i≤j≤K. The Maximum Subsequence is the continuous subsequence which has the largest sum of its elements. For example, given sequence { -2, 11, -4, 13, -5, -2 }, its maximum subsequence is { 11, -4, 13 } with the largest sum being 20.
Now you are supposed to find the largest sum, together with the first and the last numbers of the maximum subsequence.
### 输入格式
Each input file contains one test case. Each case occupies two lines. The first line contains a positive integer K (≤10000). The second line contains K numbers, separated by a space.
### 输出格式
For each test case, output in one line the largest sum, together with the first and the last numbers of the maximum subsequence. The numbers must be separated by one space, but there must be no extra space at the end of a line. In case that the maximum subsequence is not unique, output the one with the smallest indices i and j (as shown by the sample case). If all the K numbers are negative, then its maximum sum is defined to be 0, and you are supposed to output the first and the last numbers of the whole sequence.
### 输入样例
```
10
-10 1 2 3 4 -5 -23 3 7 -21
```
### 输出样例
```
10 1 4
```

### 题解
```
#include<iostream>
#include<set>
#include<string>
#include "cstring"
#include<algorithm>
#include<queue>
#include<vector>
#include "map"
#include<cmath>
using namespace std;
int a[10050],dp[10050],n,i,s[10050];
bool zheng = false;
int main() {
    cin>>n;
    for (i=0;i<n;i++)
    {
        cin>>a[i];
        if (a[i]>=0)
            zheng = true;
    }
    if (!zheng)
    {
        cout<<0<<" "<<a[0]<<" "<<a[n-1]<<endl;
        return 0;
    }
    dp[0]=a[0];
    for (i=1;i<n;i++)
    {
        if (dp[i-1]+a[i]>a[i])
        {
            dp[i] = dp[i-1]+a[i];
            s[i]=s[i-1];
        }
        else
        {
            dp[i]=a[i];
            s[i]=i;
        }
    }
    int k=0;
    for (i=1;i<n;i++)
    {
        if (dp[i]>dp[k])
            k=i;
    }
    int t=s[k]-1;
    while (a[t]==0&&t>=0)
    {
        s[k]=t--;
    }
    cout<<dp[k]<<" "<<a[s[k]]<<" "<<a[k]<<endl;
    return 0;
}
```
