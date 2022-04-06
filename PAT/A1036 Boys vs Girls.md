This time you are asked to tell the difference between the lowest grade of all the male students and the highest grade of all the female students.
### 输入格式
Each input file contains one test case. Each case contains a positive integer N, followed by N lines of student information. Each line contains a student's name, gender, ID and grade, separated by a space, where`name`and`ID`are strings of no more than 10 characters with no space,`gender`is either`F`(female) or`M`(male), and`grade`is an integer between 0 and 100. It is guaranteed that all the grades are distinct.
### 输出格式
For each test case, output in 3 lines. The first line gives the name and ID of the female student with the highest grade, and the second line gives that of the male student with the lowest grade. The third line gives the difference grade<sub>F</sub>−grade<sub>M</sub>. If one such kind of student is missing, output`Absent`in the corresponding line, and output`NA`in the third line instead.
### 输入样例1
```
3
Joe M Math990112 89
Mike M CS991301 100
Mary F EE990830 95
```
### 输出样例1
```
Mary EE990830
Joe Math990112
6
```
### 输入样例2
```
1
Jean M AA980920 60
```
### 输出样例2
```
Absent
Jean AA980920
NA
```

### 题解
```
#include <iostream>
#include <algorithm>
#include <string>
#include <cstdio>
using namespace std;
struct p
{
    string name;
    string id;
    int g;
    p(){}
    p(string a,string c,int d)
    {
        name=a;
        id=c;
        g=d;
    }
};
int main()
{
   int n,i,b,high=-1,low=1000;
   p nan,nv;
   string c,e;
   char d;
   cin>>n;
   for (i=0;i<n;i++)
   {
       cin>>c>>d>>e>>b;
       if (d=='M')
       {
           if (low>b)
           {
               low=b;
               nan=p(c,e,b);
           }
       }
       else
       {
           if (high<b)
           {
               high=b;
               nv=p(c,e,b);
           }
       }
   }
   if (high<0)
    cout<<"Absent"<<endl;
   else
    cout<<nv.name<<" "<<nv.id<<endl;
    if (low>100)
    cout<<"Absent"<<endl;
   else
    cout<<nan.name<<" "<<nan.id<<endl;
   if (high<0||low>100)
    cout<<"NA"<<endl;
   else
    cout<<high-low<<endl;
    return 0;
}
```
