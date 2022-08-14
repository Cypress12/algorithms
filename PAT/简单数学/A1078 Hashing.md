The task of this problem is simple: insert a sequence of distinct positive integers into a hash table, and output the positions of the input numbers. The hash function is defined to be H(key)=key%TSize where TSize is the maximum size of the hash table. Quadratic probing (with positive increments only) is used to solve the collisions.
Note that the table size is better to be prime. If the maximum size given by the user is not prime, you must re-define the table size to be the smallest prime number which is larger than the size given by the user.
### 输入格式
Each input file contains one test case. For each case, the first line contains two positive numbers: MSize (≤10<sup>4</sup>) and N (≤MSize) which are the user-defined table size and the number of input numbers, respectively. Then N distinct positive integers are given in the next line. All the numbers in a line are separated by a space.
### 输出格式
For each test case, print the corresponding positions (index starts from 0) of the input numbers in one line. All the numbers in a line are separated by a space, and there must be no extra space at the end of the line. In case it is impossible to insert the number, print "-" instead.
### 输入样例
```
4 4
10 6 4 15
```
### 输出样例
```
0 1 4 -
```

### 题解
```
#include<iostream>
#include<stack>
#include<string>
#include<algorithm>
#include<queue>
#include<vector>
#include<cmath>
 using namespace std;
int i,sum=0,tsize,n,t[10005],j;
bool isp(int a)
{
    if (a==1)
        return false;
    for (i=2;i<= sqrt(a);i++)
    {
        if (a%i==0)
            return false;
    }
    return true;
}
int findp(int a)
{
    for (i=a+1;;i++)
    {
        if (i==2)
            return i;
        bool flag= true;
        for (j=2;j<= sqrt(i);j++)
        {
            if (i%j==0)
            {
                flag= false;
                break;
            }
        }
        if (flag)
            return i;
    }
}
 int main()
 {
     cin>>tsize>>n;
    if (isp(tsize)== false)
    {
        tsize = findp(tsize);
    }
     for (i=0;i<n;i++)
     {
         int tt;
         cin>>tt;
         int index = tt%tsize;
         for (j=1;j<=tsize;j++)
         {
             if (t[index]==0)
             {
                 t[index] = tt;
                 break;
             }
             index = tt + pow(j,2) ;
             index %= tsize;
         }
         if (t[index]!=tt)
             cout<<"-";
         else
            cout<<index;
         if (i!=n-1)
             cout<<" ";
     }
    return 0;
 }
```
