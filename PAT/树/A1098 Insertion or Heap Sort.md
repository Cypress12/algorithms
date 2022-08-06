给出一个初始序列，可以对它使用插入排序或堆排序。现在给出一个序列，判断它是由插入排序还是由堆排序产生的，并输出下一步将会产生的序列
### 输入格式
Each input file contains one test case. For each case, the first line gives a positive integer N (≤100). Then in the next line, N integers are given as the initial sequence. The last line contains the partially sorted sequence of the N numbers. It is assumed that the target sequence is always ascending. All the numbers in a line are separated by a space.
### 输出格式
For each test case, print in the first line either "Insertion Sort" or "Heap Sort" to indicate the method used to obtain the partial result. Then run this method for one more iteration and output in the second line the resulting sequence. It is guaranteed that the answer is unique for each test case. All the numbers in a line must be separated by a space, and there must be no extra space at the end of the line.
### 输入样例1
```
10
3 1 2 8 7 5 9 4 6 0
1 2 3 7 8 5 9 4 6 0
```
### 输出样例1
```
Insertion Sort
1 2 3 5 7 8 9 4 6 0
```
### 输入样例2
```
10
3 1 2 8 7 5 9 4 6 0
6 4 5 1 0 3 2 7 8 9
```
### 输出样例2
```
Heap Sort
5 4 3 1 0 2 6 7 8 9
```

### 题解
```
#include <cstdio>
#include <cstring>
#include <algorithm>
#include <queue>
#include <iostream>
#include <vector>
using namespace std;
int a[105],b[105],c[105];
int i,n,j;
bool flag = false;
void downadjust(int low, int high)
{
    int k=low,l=low*2+1;
    while(l<=high)
    {
        if (l+1<=high&&b[l]<b[l+1])
            l=l+1;
        if (b[l]>b[k])
        {
            swap(b[l],b[k]);
            k=l;
            l=k*2+1;
        }
        else
            break;
    }
}
bool eq(int a[],int b[])
{
    for (int i=0;i<n;i++)
    {
        if (a[i]!=b[i])
            return false;
    }
    return true;
}
int main()
{
  cin>>n;
  for (i=0;i<n;i++)
  {
     int t;
     cin>>t;
     a[i]=t;
     b[i]=t;
  }
  for (i=0;i<n;i++)
  {
      int t;
      cin>>t;
      c[i]=t;
  }
  for (i=1;i<n;i++)
  {
      sort(a,a+i+1);
      if (flag)
      {
          for (j=0;j<n;j++)
          {
              cout<<a[j];
              if (j!=n-1)
                cout<<" ";
          }
          return 0;
      }
      if (eq(a,c))
      {
          cout<<"Insertion Sort"<<endl;
          flag=true;
      }
  }
    for (i=n/2-1;i>=0;i--)
    {
        downadjust(i,n-1);
    }
    for (i=n-1;i>0;i--)
    {
        swap(b[i],b[0]);
        downadjust(0,i-1);
        if (flag)
        {
            for (j=0;j<n;j++)
          {
              cout<<b[j];
              if (j!=n-1)
                cout<<" ";
          }
            break;
        }
        if (eq(b,c))
        {
            cout<<"Heap Sort"<<endl;
            flag=true;
        }

    }
    return 0;
}
```
