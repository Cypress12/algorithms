给定一个长度不超过 10<sup>4</sup>的、仅由英文字母构成的字符串。请将字符重新调整顺序，按 `PATestPATest....` 这样的顺序输出，并忽略其它字符。当然，六种字符的个数不一定是一样多的，若某种字符已经输出完，则余下的字符仍按 PATest 的顺序打印，直到所有字符都被输出。
### 输入格式
输入在一行中给出一个长度不超过 10<sup>4</sup>的、仅由英文字母构成的非空字符串。
### 输出格式
在一行中按题目要求输出排序后的字符串。题目保证输出非空。
### 输入样例
```
redlesPayBestPATTopTeePHPereatitAPPT
```
### 输出样例
```
PATestPATestPTetPTePePee
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
char dic[6]={'P','A','T','e','s','t'};
int sc[6];
int chazhao(char a)
{
    int i;
    for (i=0;i<6;i++)
    {
        if (a==dic[i])
            return i;
    }
    return -1;
}
string b;
int main()
{
   cin>>b;
   int i;
   for (i=0;i<b.length();i++)
   {
       int ind = chazhao(b[i]);
       if (ind!=-1)
        sc[ind]++;
   }
   while(true)
   {
       bool flag=true;
       for (i=0;i<6;i++)
       {
           if (sc[i]>0)
           {
               printf("%c",dic[i]);
               sc[i]--;
               flag=false;
           }
       }
       if (flag)
        break;
   }
    return 0;
}
```
