People in Mars represent the colors in their computers in a similar way as the Earth people. That is, a color is represented by a 6-digit number, where the first 2 digits are for Red, the middle 2 digits for Green, and the last 2 digits for Blue. The only difference is that they use radix 13 (0-9 and A-C) instead of 16. Now given a color in three decimal numbers (each between 0 and 168), you are supposed to output their Mars RGB values.
### 输入格式
Each input file contains one test case which occupies a line containing the three decimal color values.
### 输出格式
For each test case you should output the Mars RGB value in the following format: first output`#`, then followed by a 6-digit number where all the English characters must be upper-cased. If a single color is only 1-digit long, you must print a`0`to its left.
### 输入样例
```
15 43 71
```
### 输出样例
```
#123456
```

### 题解
```
#include <iostream>
#include <vector>
#include <string>
#include <cstdio>
using namespace std;
char s[3]={'A','B','C'};

int main() {
    int a,i,j;
    printf("#");
    for(i=0;i<3;i++)
    {
        scanf("%d",&a);
        int ans[2],sum=0;
        do
        {
            ans[sum++]=a%13;
            a/=13;
        }while(a>0);
        if (sum==1) ans[1]=0;
        for (j=1;j>=0;j--)
        {
            if (ans[j]>=10)
            {
                printf("%c",s[ans[j]-10]);
            }
            else
            printf("%d",ans[j]);
        }
    }


    return 0;
}
```
