The Japanese language is notorious for its sentence ending particles. Personal preference of such particles can be considered as a reflection of the speaker's personality. Such a preference is called "Kuchiguse" and is often exaggerated artistically in Anime and Manga. For example, the artificial sentence ending particle "nyan~" is often used as a stereotype for characters with a cat-like personality:
Itai nyan~ (It hurts, nyan~)
Ninjin wa iyada nyan~ (I hate carrots, nyan~)
Now given a few lines spoken by the same character, can you find her Kuchiguse?
### 输入格式
Each input file contains one test case. For each case, the first line is an integer N (2≤N≤100). Following are N file lines of 0~256 (inclusive) characters in length, each representing a character's spoken line. The spoken lines are case sensitive.
### 输出格式
For each test case, print in one line the kuchiguse of the character, i.e., the longest common suffix of all N lines. If there is no such suffix, write`nai`.
### 输入样例1
```
3
Itai nyan~
Ninjin wa iyadanyan~
uhhh nyan~
```
### 输出样例1
```
nyan~
```
### 输入样例2
```
3
Itai!
Ninjinnwaiyada T_T
T_T
```
### 输出样例2
```
nai
```

### 题解
```
#带空格输入用getline
#cin用getchar吸收空格
#include <iostream>
#include <algorithm>
#include <string>
#include <cstdio>
#include <climits>
#include <cstring>
using namespace std;
string a[101];
int publen = INT_MAX;
bool judge(char a,char b)
{
    return a==b;
}
int main()
{
   int n,i,j;
   cin>>n;
   getchar();
   for (i=0;i<n;i++)
   {
       getline(cin,a[i]);
       reverse(a[i].begin(),a[i].end());
       if (a[i].length()<publen) publen =a[i].length();
   }
   string t;
   bool flag = false;
   for (i=0;i<publen;i++)
   {
       for (j=1;j<n;j++)
       {
           char c = a[0][i],d=a[j][i];
           if (!judge(c,d))
           {
               flag = true;
               break;
           }
       }
       if (flag) break;
       else t += a[0][i];
   }
   reverse(t.begin(),t.end());
   if (t.length()) cout<<t<<endl;
   else
    cout<<"nai"<<endl;
    return 0;
}
```
