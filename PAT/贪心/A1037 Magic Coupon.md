给出两个集合，从这两个集合中分别选取相同数量的元素进行一对一相乘，问能达到的乘积之和最大是多少
### 输入格式
Each input file contains one test case. For each case, the first line contains the number of coupons N<sub>C</sub>, followed by a line with N<sub>C</sub>coupon integers. Then the next line contains the number of products N<sub>P</sub>, followed by a line with N<sub>P</sub>product values. Here 1≤N<sub>C</sub>,N<sub>P</sub>≤10<sup>5</sup>, and it is guaranteed that all the numbers will not exceed 2<sup>30</sup>.
### 输出格式
For each test case, simply print in a line the maximum amount of money you can get back.
### 输入样例
```
4
1 2 4 -1
4
7 6 -2 -3
```
### 输出样例
```
43
```

### 题解
```
#include <iostream>
#include <vector>
#include <string>
#include <cstdio>
#include <cmath>
#include <algorithm>
using namespace std;
int n,m,a1[100005],a2[100005],b1[100005],b2[100005],a11=0,a21=0,b11=0,b21=0,i;

int main()
{
    cin>>n;
    for (i=0;i<n;i++)
    {
        int t;
        cin>>t;
        if (t>=0)
            a1[a11++]=t;
        else
            a2[a21++]=t;
    }
    cin>>m;
    for (i=0;i<m;i++)
    {
        int t;
        cin>>t;
        if (t>=0)
            b1[b11++]=t;
        else
            b2[b21++]=t;
    }
    int zheng=min(a11,b11);
    int fu=min(a21,b21);
    long long ans=0;
    sort(a1,a1+a11);
    sort(b1,b1+b11);
    sort(a2,a2+a21);
    reverse(a1,a1+a11);
    sort(b2,b2+b21);
    reverse(b1,b1+b11);
    for(i=0;i<zheng;i++)
        ans+=a1[i]*b1[i];
    for(i=0;i<fu;i++)
    {
        ans+=b2[i]*a2[i];
    }
    cout<<ans<<endl;
    return 0;
}
```
