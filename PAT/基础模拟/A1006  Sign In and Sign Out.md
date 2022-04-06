At the beginning of every day, the first person who signs in the computer room will unlock the door, and the last one who signs out will lock the door. Given the records of signing in's and out's, you are supposed to find the ones who have unlocked and locked the door on that day.
### 输入格式
Each input file contains one test case. Each case contains the records for one day. The case starts with a positive integer M, which is the total number of records, followed by M lines, each in the format:
`ID_number Sign_in_time Sign_out_time`
where times are given in the format`HH:MM:SS`, and`ID_number`is a string with no more than 15 characters.
### 输出格式
For each test case, output in one line the ID numbers of the persons who have unlocked and locked the door on that day. The two ID numbers must be separated by one space.
Note: It is guaranteed that the records are consistent. That is, the sign in time must be earlier than the sign out time for each person, and there are no two persons sign in or out at the same moment.
### 输入样例
```
3
CS301111 15:30:28 17:00:10
SC3021234 08:00:00 11:25:25
CS301133 21:45:00 21:58:40
```
### 输出样例
```
SC3021234 CS301133
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
    string kai;
    string guan;
}a[1<<10];
p lai,qu;
int main()
{
   int i,n;
   cin>>n;
   lai.kai="60:60:60";
   qu.guan="00:00:00";
   for (i=0;i<n;i++)
   {
       cin>>a[i].name>>a[i].kai>>a[i].guan;
       if (lai.kai>a[i].kai)
        lai=a[i];
       if (qu.guan<a[i].guan)
        qu=a[i];
   }
    cout<<lai.name<<" "<<qu.name<<endl;
    return 0;
}
```
