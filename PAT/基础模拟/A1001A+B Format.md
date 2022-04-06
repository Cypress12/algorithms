Calculate a+b and output the sum in standard format -- that is, the digits must be separated into groups of three by commas (unless there are less than four digits).
### 输入格式
Each input file contains one test case. Each case contains a pair of integers a and b where −10<sup>6</sup>≤a,b≤10<sup>6</sup>. The numbers are separated by a space.
### 输出格式
For each test case, you should output the sum of a and b in one line. The sum must be written in the standard format.
### 输入样例
```
-1000000 9
```
### 输出样例
```
-999,991
```

### 题解
```
#include <iostream>
#include <algorithm>
#include <string>
#include <cstdio>
using namespace std;
string a;
int main()
{
   long long d,b;
   cin>>d>>b;
   int i=1,sum=d+b,t=abs(sum);
   do
   {
       a+=t%10+'0';
       if (i%3==0 && t>9)
        a+=',';
       t/=10;
       i++;
   }while(t>0);
   reverse(a.begin(),a.end());
   if (sum<0)
   {
       cout<<'-';
   }
    int j;
   cout<<a;
    return 0;
}
```
