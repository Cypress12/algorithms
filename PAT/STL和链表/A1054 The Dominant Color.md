Behind the scenes in the computer's memory, color is always talked about as a series of 24 bits of information for each pixel. In an image, the color with the largest proportional area is called the dominant color. A strictly dominant color takes more than half of the total area. Now given an image of resolution M by N (for example, 800×600), you are supposed to point out the strictly dominant color.
### 输入格式
Each input file contains one test case. For each case, the first line contains 2 positive numbers: M (≤800) and N (≤600) which are the resolutions of the image. Then N lines follow, each contains M digital colors in the range [0,2<sup>24</sup>). It is guaranteed that the strictly dominant color exists for each input image. All the numbers in a line are separated by a space.
### 输出格式
For each test case, simply print the dominant color in a line.
### 输入样例
```
5 3
0 0 255 16777215 24
24 24 0 0 24
24 0 24 24 24
```
### 输出样例
```
24
```

### 题解
```
#include <iostream>
#include <vector>
#include <string>
#include <cstdio>
#include <cmath>
#include <algorithm>
#include <map>
using namespace std;
map<int,int>a;
map<int,int>::iterator it;
int n,m,i,j,r,sum=-1;
int main()
{
   cin>>n>>m;
   for (i=0;i<m;i++)
   {
       for (j=0;j<n;j++)
       {
           int t;
           cin>>t;
           if (a.find(t)!=a.end())
            a[t]++;
           else
            a[t]=1;
       }
   }
   for (it=a.begin();it!=a.end();it++)
   {
       if (it->second>sum && it->second>m*n/2)
        {
            sum=it->second;
            r=it->first;
        }
   }
   cout<<r<<endl;
    return 0;
}
```
