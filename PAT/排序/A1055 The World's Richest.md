Forbes magazine publishes every year its list of billionaires based on the annual ranking of the world's wealthiest people. Now you are supposed to simulate this job, but concentrate only on the people in a certain range of ages. That is, given the net worths of N people, you must find the M richest people in a given range of their ages.
### 输入格式
Each input file contains one test case. For each case, the first line contains 2 positive integers: N (≤10<sup>5</sup>) - the total number of people, and K (≤10<sup>3</sup>) - the number of queries. Then N lines follow, each contains the name (string of no more than 8 characters without space), age (integer in (0, 200]), and the net worth (integer in [−10<sup>6</sup>,10<sup>6</sup>]) of a person. Finally there are K lines of queries, each contains three positive integers: M (≤100) - the maximum number of outputs, and [Amin, Amax] which are the range of ages. All the numbers in a line are separated by a space.
### 输出格式
For each query, first print in a line `Case #X:` where X is the query number starting from 1. Then output the M richest people with their ages in the range [Amin, Amax]. Each person's information occupies a line, in the format
```
Name Age Net_Worth
```
The outputs must be in non-increasing order of the net worths. In case there are equal worths, it must be in non-decreasing order of the ages. If both worths and ages are the same, then the output must be in non-decreasing alphabetical order of the names. It is guaranteed that there is no two persons share all the same of the three pieces of information. In case no one is found, output `None`.
### 输入样例
```
12 4
Zoe_Bill 35 2333
Bob_Volk 24 5888
Anny_Cin 95 999999
Williams 30 -22
Cindy 76 76000
Alice 18 88888
Joe_Mike 32 3222
Michael 5 300000
Rosemary 40 5888
Dobby 24 5888
Billy 24 5888
Nobody 5 0
4 15 45
4 30 35
4 5 95
1 45 50
```
### 输出样例
```
Case #1:
Alice 18 88888
Billy 24 5888
Bob_Volk 24 5888
Dobby 24 5888
Case #2:
Joe_Mike 32 3222
Zoe_Bill 35 2333
Williams 30 -22
Case #3:
Anny_Cin 95 999999
Michael 5 300000
Alice 18 88888
Cindy 76 76000
Case #4:
None
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
struct xuesheng
{
    string name;
    int age;
    int worth;
}s[100005];
bool cmp(xuesheng a,xuesheng b)
{
    if (a.worth!=b.worth)
        return a.worth>b.worth;
    else if (a.age!=b.age)
        return a.age<b.age;
    else
        return a.name<b.name;
}
int n,m,i,num,l,r,j;
int main()
{
    scanf("%d %d",&n,&m);
    for (i=0;i<n;i++)
    {
        cin>>s[i].name;
        scanf("%d %d",&s[i].age,&s[i].worth);
    }
    sort(s,s+n,cmp);
    for (i=1;i<=m;i++)
    {
        scanf("%d %d %d",&num,&l,&r);
        printf("Case #%d:\n",i);
        bool flag = true;
        for (j=0;j<n;j++)
        {
            if (num==0)
                break;
            if (s[j].age>=l && s[j].age<=r)
            {
                cout<<s[j].name;
                printf(" %d %d\n",s[j].age,s[j].worth);
                num--;
                flag = false;
            }
        }
        if (flag) printf("None\n");
    }
    return 0;
}
```
