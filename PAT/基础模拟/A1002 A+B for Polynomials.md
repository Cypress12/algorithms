This time, you are supposed to find A+B where A and B are two polynomials.
### 输入格式
Each input file contains one test case. Each case occupies 2 lines, and each line contains the information of a polynomial:
KN<sub>1aN1</sub>N<sub>2aN2</sub>...N<sub>KaNK</sub>where K is the number of nonzero terms in the polynomial, N<sub>i</sub>and<sub>aNi</sub>(i=1,2,⋯,K) are the exponents and coefficients, respectively. It is given that 1≤K≤10，0≤N<sub>K</sub><⋯<N<sub>2</sub><N<sub>1</sub>≤1000.
### 输出格式
For each test case you should output the sum of A and B in one line, with the same format as the input. Notice that there must be NO extra space at the end of each line. Please be accurate to 1 decimal place.
### 输入样例
```
2 1 2.4 0 3.2
2 2 1.5 1 0.5
```
### 输出样例
```
3 2 1.5 1 2.9 0 3.2
```

### 题解
```
#include <iostream>
#include <algorithm>
#include <cmath>
#include <cstdio>
using namespace std;
double a[1005],sum=0;
int main()
{
    int b,i,n;
    double c;
    cin>>n;
    while(n--)
    {
        cin>>b>>c;
        a[b]=c;
        sum++;
    }
    cin>>n;
    while(n--)
    {
        cin>>b>>c;
        if (a[b]==0)
        {
            sum++;
            a[b]=c;
        }
        else
        {
            a[b]+=c;
            if (a[b]==0) sum--;
        }
    }
    cout<<sum;
    if (sum) cout<<" ";
    for (i=1000; i>=0; i--)
    {
        if (a[i]!=0)
        {
            cout<<i<<" ";
            printf("%.1f",a[i]);
            sum--;
            if (sum) cout<<" ";
        }
    }
    return 0;
}

```
