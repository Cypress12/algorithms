Given a list of N student records with name, ID and grade. You are supposed to sort the records with respect to the grade in non-increasing order, and output those student records of which the grades are in a given interval.
### 输入格式
Each input file contains one test case. Each case is given in the following format:
```
N
name[1] ID[1] grade[1]
name[2] ID[2] grade[2]
... ...
name[N] ID[N] grade[N]
grade1 grade2
```
where `name[i]` and `ID[i]` are strings of no more than 10 characters with no space,` grade[i]` is an integer in [0, 100], `grade1` and `grade2` are the boundaries of the grade's interval. It is guaranteed that all the grades are distinct.
### 输出格式
For each test case you should output the student records of which the grades are in the given interval [`grade1`, `grade2`] and are in non-increasing order. Each student record occupies a line with the student's name and ID, separated by one space. If there is no student's grade in that interval, output `NONE` instead.
### 输入样例1
```
4
Tom CS000001 59
Joe Math990112 89
Mike CS991301 100
Mary EE990830 95
60 100
```
### 输出样例1
```
Mike CS991301
Mary EE990830
Joe Math990112
```
### 输入样例2
```
2
Jean AA980920 60
Ann CS01 80
90 95
```
### 输出样例2
```
NONE
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
#include <sstream>
using namespace std;
struct xuesheng
{
    string name;
    string id;
    int score;
}s[10005];
bool cmp(xuesheng a,xuesheng b)
{
    if (a.score!=b.score) return a.score>b.score;
}
int n,m,i,num,l,r,j,proscore[6];

int main()
{
    scanf("%d",&n);
    for (i=0;i<n;i++)
    {
        cin>>s[i].name>>s[i].id>>s[i].score;
    }
    scanf("%d %d",&l,&r);
    sort(s,s+n,cmp);
    bool flag = true;
    for (i=0;i<n;i++)
    {
        if (s[i].score>=l&&s[i].score<=r)
        {
            cout<<s[i].name<<" "<<s[i].id<<endl;
            flag=false;
        }
    }
    if (flag) cout<<"NONE"<<endl;
    return 0;
}
```
