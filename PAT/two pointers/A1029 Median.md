Given an increasing sequence S of N integers, the median is the number at the middle position. For example, the median of S1 = { 11, 12, 13, 14 } is 12, and the median of S2 = { 9, 10, 15, 16, 17 } is 15. The median of two sequences is defined to be the median of the nondecreasing sequence which contains all the elements of both sequences. For example, the median of S1 and S2 is 13.
Given two increasing sequences of integers, you are asked to find their median.
### 输入格式
Each input file contains one test case. Each case occupies 2 lines, each gives the information of a sequence. For each sequence, the first positive integer N (≤2×10<sup>5</sup>) is the size of that sequence. Then N integers follow, separated by a space. It is guaranteed that all the integers are in the range of long int.
### 输出格式
For each test case you should output the median of the two given sequences in a line.
### 输入样例
```
4 11 12 13 14
5 9 10 15 16 17
```
### 输出样例
```
13
```

### 题解
```
#include <iostream>
#include <algorithm>
#include <string>
#include <cstdio>
#include <climits>
#include <cstring>
#include <sstream>
#include <cmath>
using namespace std;
long long a[200005],b[200005],n,m;
int main()
{
  int i;
  cin>>n;
  for (i=0;i<n;i++)
    cin>>a[i];
  cin>>m;
  for (i=0;i<m;i++)
    cin>>b[i];
  long long j,k,l,c;
  if ((m+n)%2==0) c=(m+n)/2;
  else c=(m+n)/2+1;
  for (i=0,j=0,k=0;i<n&&j<m&&k<c;k++)
  {
      if (a[i]>=b[j]) l=b[j],j++;
      else l=a[i],i++;
  }
  if (k<c)
  {
      while(i<n&&k<c)
      {
          l=a[i];
          k++;
          i++;
      }
      while(j<m&&k<c)
      {
          l=b[j];
          j++,k++;
      }
  }
  cout<<l<<endl;
    return 0;
}
```
