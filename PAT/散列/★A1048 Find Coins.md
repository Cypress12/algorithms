Eva loves to collect coins from all over the universe, including some other planets like Mars. One day she visited a universal shopping mall which could accept all kinds of coins as payments. However, there was a special requirement of the payment: for each bill, she could only use exactly two coins to pay the exact amount. Since she has as many as 10<sup>5</sup>coins with her, she definitely needs your help. You are supposed to tell her, for any given amount of money, whether or not she can find two coins to pay for it.
### 输入格式
Each input file contains one test case. For each case, the first line contains 2 positive numbers: N (≤10<sup>5</sup>, the total number of coins) and M (≤10<sup>3</sup>, the amount of money Eva has to pay). The second line contains N face values of the coins, which are all positive numbers no more than 500. All the numbers in a line are separated by a space.
### 输出格式
For each test case, print in one line the two face values V<sub>1</sub>and V<sub>2</sub>(separated by a space) such that V<sub>1</sub>+V<sub>2</sub>=M and V<sub>1</sub>≤V<sub>2</sub>. If such a solution is not unique, output the one with the smallest V<sub>1</sub>. If there is no solution, output `No Solution` instead.
### 输入样例1
```
8 15
1 2 8 7 2 4 11 15
```
### 输出样例1
```
4 11
```
### 输入样例2
```
7 14
1 8 7 2 4 11 15
```
### 输出样例2
```
No Solution
```

### 题解
```
#include <iostream>
#include <algorithm>
#include <string>
#include <cstdio>
#include <climits>
#include <cstring>
#include <cmath>
using namespace std;
int n,m,sc[100005],i;
int main()
{
   memset(sc,0,sizeof(sc));
   cin>>n>>m;
   bool flag=true;
   for (i=0;i<n;i++)
   {
       int t;
       cin>>t;
       sc[t]++;
   }
   for (i=1;i<=m;i++)
   {
       if (sc[i]>0&&sc[m-i]>0)
       {
           if ((i==m-i&&sc[i]>1&&sc[m-i]>1)||(i!=m-i))
            {
                cout<<i<<" "<<m-i<<endl;
                flag=false;
                break;
            }
       }
   }
   if (flag) printf("No Solution");
    return 0;
}
```
