Given any permutation of the numbers {0, 1, 2,..., N−1}, it is easy to sort them in increasing order. But what if `Swap(0, *)` is the ONLY operation that is allowed to use? For example, to sort {4, 0, 2, 1, 3} we may apply the swap operations in the following way:
```
Swap(0, 1) => {4, 1, 2, 0, 3}
Swap(0, 3) => {4, 1, 2, 3, 0}
Swap(0, 4) => {0, 1, 2, 3, 4}
```
Now you are asked to find the minimum number of swaps need to sort the given permutation of the first N nonnegative integers.
### 输入格式
Each input file contains one test case, which gives a positive N (≤10<sup>5</sup>) followed by a permutation sequence of {0, 1, ..., N−1}. All the numbers in a line are separated by a space.
### 输出格式
For each case, simply print in a line the minimum number of swaps need to sort the given permutation.
### 输入样例
```
10
3 5 7 2 6 4 9 0 8 1
```
### 输出样例
```
9
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
int num[100005],ans=0,n,i,lef,k=1;
int main()
{
    cin>>n;
    lef=n-1;
    for (i=0;i<n;i++)
    {
        int a;
        cin>>a;
        num[a]=i;
        if (a==i&&i!=0) lef--;
    }
    while(lef)
    {
        if(lef&&num[0]==0)
        {
            while(k<n)
            {
                if (num[k]!=k)
                {
                    swap(num[0],num[k]);
                    ans++;
                    break;
                }
                k++;
            }
        }
        while(num[0])
        {
            swap(num[0],num[num[0]]);
            ans++;
            lef--;
        }
    }
    cout<<ans<<endl;
    return 0;
}
```
