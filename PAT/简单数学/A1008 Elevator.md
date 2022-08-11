The highest building in our city has only one elevator. A request list is made up with N positive numbers. The numbers denote at which floors the elevator will stop, in specified order. It costs 6 seconds to move the elevator up one floor, and 4 seconds to move down one floor. The elevator will stay for 5 seconds at each stop.
For a given request list, you are to compute the total time spent to fulfill the requests on the list. The elevator is on the 0th floor at the beginning and does not have to return to the ground floor when the requests are fulfilled.
### 输入格式
Each input file contains one test case. Each case contains a positive integer N, followed by N positive numbers. All the numbers in the input are less than 100.
### 输出格式
For each test case, print the total time on a single line.
### 输入样例
```
3 2 3 1
```
### 输出样例
```
41
```

### 题解
```
#include <cstdio>
#include <cstring>
#include <algorithm>
#include <cmath>
#include <queue>
#include <iostream>
#include <vector>
using namespace std;
int n,sum=0,t,now=0,i;

int main()
{
   cin>>n;
   for (i=0;i<n;i++)
   {
       cin>>t;
       int tt;
       if (t-now>0)
           tt=6;
       else
           tt=4;
       sum += abs(t-now)*tt+5;
       now=t;
   }
   cout<<sum<<endl;
    return 0;
}
```
