Excel can sort records according to any column. Now you are supposed to imitate this function.
### 输入格式
Each input file contains one test case. For each case, the first line contains two integers N (≤10<sup>5</sup>) and C, where N is the number of records and C is the column that you are supposed to sort the records with. Then N lines follow, each contains a record of a student. A student's record consists of his or her distinct ID (a 6-digit number), name (a string with no more than 8 characters without space), and grade (an integer between 0 and 100, inclusive).
### 输出格式
For each test case, output the sorting result in N lines. That is, if C = 1 then the records must be sorted in increasing order according to ID's; if C = 2 then the records must be sorted in non-decreasing order according to names; and if C = 3 then the records must be sorted in non-decreasing order according to grades. If there are several students who have the same name or grade, they must be sorted according to their ID's in increasing order.
### 输入样例1
```
3 1
000007 James 85
000010 Amy 90
000001 Zoe 60
```
### 输出样例1
```
000001 Zoe 60
000007 James 85
000010 Amy 90
```
### 输入样例2
```
4 2
000007 James 85
000010 Amy 90
000001 Zoe 60
000002 James 98
```
### 输出样例2
```
000010 Amy 90
000002 James 98
000007 James 85
000001 Zoe 60
```
### 输入样例3
```
4 3
000007 James 85
000010 Amy 90
000001 Zoe 60
000002 James 9
```
### 输出样例3
```
000002 James 9
000001 Zoe 60
000007 James 85
000010 Amy 90
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
    int id;
    string name;
    int score;
}s[100005];
int n,m,i,j;
bool cmp1(xuesheng a,xuesheng b)
{
    if(a.id!=b.id) return a.id<b.id;
}
bool cmp2(xuesheng a,xuesheng b)
{
    if (a.name!=b.name)
        return a.name<b.name;
    else return a.id<b.id;
}
bool cmp3(xuesheng a,xuesheng b)
{
    if (a.score!=b.score)
    {
        return a.score<b.score;
    }
    else
        return a.id<b.id;
}
int main()
{
    scanf("%d %d",&n,&m);
    for (i=0;i<n;i++)
    {
        scanf("%d",&s[i].id);
        cin>>s[i].name;
        scanf("%d",&s[i].score);
    }
    if (m==1)
        sort(s,s+n,cmp1);
    else if (m==2)
        sort(s,s+n,cmp2);
    else
        sort(s,s+n,cmp3);
    for (i=0;i<n;i++)
        printf("%06d %s %d\n",s[i].id,s[i].name.c_str(),s[i].score);
    return 0;
}
```
