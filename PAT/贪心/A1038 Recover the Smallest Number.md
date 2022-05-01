Given a collection of number segments, you are supposed to recover the smallest number from them. For example, given { 32, 321, 3214, 0229, 87 }, we can recover many numbers such like 32-321-3214-0229-87 or 0229-32-87-321-3214 with respect to different orders of combinations of these segments, and the smallest number is 0229-321-3214-32-87.
### 输入格式
Each input file contains one test case. Each case gives a positive integer N (≤10<sup>4</sup>) followed by N number segments. Each segment contains a non-negative integer of no more than 8 digits. All the numbers in a line are separated by a space.
### 输出格式
For each test case, print the smallest number in one line. Notice that the first digit must not be zero.
### 输入样例
```
5 32 321 3214 0229 87
```
### 输出样例
```
22932132143287
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
string a[10005];
int n,i;
bool cmp(string a,string b)
{
    return a+b<b+a;
}
int main()
{
    cin>>n;
    for (i=0;i<n;i++)
        cin>>a[i];
    sort(a,a+n,cmp);
    string s,t;
    bool flag=true;
    for (i=0;i<n;i++)
    {
        s+=a[i];
    }
    for (i=0;i<s.length();i++)
    {
        if (flag&&s[i]=='0')
        {
            continue;
        }
        else
        {
            flag=false;
            t+=s[i];
        }
    }
    if (t.length())
        cout<<t;
    else
        cout<<0;
    return 0;
}
```
