The task is really simple: given N exits on a highway which forms a simple cycle, you are supposed to tell the shortest distance between any pair of exits.
### 输入格式
Each input file contains one test case. For each case, the first line contains an integer N (in [3,10<sup>5</sup>]), followed by N integer distances D<sub>1</sub>D<sub>2</sub>⋯D<sub>N</sub>, where D<sub>i</sub>is the distance between the i-th and the (i+1)-st exits, and D<sub>N</sub>is between the N-th and the 1st exits. All the numbers in a line are separated by a space. The second line gives a positive integer M (≤10<sup>4</sup>), with M lines follow, each contains a pair of exit numbers, provided that the exits are numbered from 1 to N. It is guaranteed that the total round trip distance is no more than 10<sup>7</sup>.
### 输出格式
For each test case, print your results in M lines, each contains the shortest distance between the corresponding given pair of exits.
### 输入样例
```
5 1 2 4 14 9
3
1 3
2 5
4 1
```
### 输出样例
```
3
10
7
```

### 题解
```
#include <iostream>
#include <algorithm>
#include <cmath>
#include <cstdio>
using namespace std;
int sum=0,d[100005],a[100005];
int main()
{
   int i,n;
   cin>>n;
   for (i=1;i<=n;i++)
   {
       cin>>a[i];
       sum+=a[i];
       d[i]=sum;
   }
   cin>>n;
   int l,r;
   while(n--)
   {
       cin>>l>>r;
       if (l>r) swap(l,r);
       int t=d[r-1]-d[l-1];
       cout<<min(t,sum-t)<<endl;
   }
    return 0;
}
```
