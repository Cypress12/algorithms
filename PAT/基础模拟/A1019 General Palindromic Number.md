给出两个整数n、b，问十进制整数n在b进制下是否是回文数，若是输出Yes，否则输出No。在此之后输出n在b进制下的表示
### 输入格式
Each input file contains one test case. Each case consists of two positive numbers N and b, where 0<N≤10<sup>9</sup>is the decimal number and 2≤b≤10<sup>9</sup>is the base. The numbers are separated by a space.
### 输出格式
For each test case, first print in one line`Yes`if N is a palindromic number in base b, or`No`if not. Then in the next line, print N as the number in base b in the form "a<sub>k</sub>a<sub>k−1</sub>...a<sub>0</sub>". Notice that there must be no extra space at the end of output.
### 输入样例1
```
27 2
```
### 输出样例1
```
Yes
1 1 0 1 1
```
### 输入样例2
```
121 5
```
### 输出样例2
```
No
4 4 1
```

### 题解
```
#include <iostream>
#include <vector>
#include <string>
#include <cstdio>
using namespace std;
int ans[100000000];

int main() {
    int a,d,sum=0,i,j;
    bool flag=true;
    scanf("%d %d",&a,&d);
    do{
       ans[sum++]=a%d;
       a/=d;
    }while(a>0);
    for (i=0,j=sum-1;i<sum/2;i++)
    {
        if (ans[i]!=ans[j])
        {
            flag = false;
            break;
        }
        j--;
    }
    if (flag) printf("Yes\n");
    else printf("No\n");
    for (int i=sum-1;i>=0;i--)
    {
        printf("%d",ans[i]);
        if (i!=0) printf(" ");
    }
    return 0;
}
```
