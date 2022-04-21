Programming Ability Test (PAT) is organized by the College of Computer Science and Technology of Zhejiang University. Each test is supposed to run simultaneously in several places, and the ranklists will be merged immediately after the test. Now it is your job to write a program to correctly merge all the ranklists and generate the final rank.
### 输入格式
Each input file contains one test case. For each case, the first line contains a positive number N (≤100), the number of test locations. Then N ranklists follow, each starts with a line containing a positive integer K (≤300), the number of testees, and then K lines containing the registration number (a 13-digit number) and the total score of each testee. All the numbers in a line are separated by a space.
### 输出格式
For each test case, first print in one line the total number of testees. Then print the final ranklist in the following format:
```
registration_number final_rank location_number local_rank
```
The locations are numbered from 1 to N. The output must be sorted in nondecreasing order of the final ranks. The testees with the same score must have the same rank, and the output must be sorted in nondecreasing order of their registration numbers.
### 输入样例
```
2
5
1234567890001 95
1234567890005 100
1234567890003 95
1234567890002 77
1234567890004 85
4
1234567890013 65
1234567890011 25
1234567890014 100
1234567890012 85
```
### 输出样例
```
9
1234567890005 1 1 1
1234567890014 1 2 1
1234567890001 3 1 2
1234567890003 3 1 2
1234567890004 5 1 4
1234567890012 5 2 2
1234567890002 7 1 5
1234567890013 8 2 3
1234567890011 9 2 4
```

### 题解
```
#id用字符类型储存 不能用数字类型
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
    char id[15];
    int score;
    int kaochanghao;
    int kaochangrank;
    int totalrank;
}s[100000];
bool cmp(xuesheng a,xuesheng b)
{
    if (a.score!=b.score)
        return a.score>b.score;
    else
        return strcmp(a.id,b.id)<0;
}
int numkaochang,personnum,i,j,sum=0,k;
int main()
{
  scanf("%d",&numkaochang);
  for (i=0;i<numkaochang;i++)
  {
      scanf("%d",&personnum);
      for (j=sum;j<sum+personnum;j++)
      {
          scanf("%s %d",s[j].id,&s[j].score);
          s[j].kaochanghao = i+1;
      }
      sort(s+sum,s+sum+personnum,cmp);
      for (j=sum,k=1;j<sum+personnum;j++,k++)
      {
          if (j==sum || s[j].score!= s[j-1].score) s[j].kaochangrank=k;
          else s[j].kaochangrank = s[j-1].kaochangrank;
      }
      sum+=personnum;
  }
  sort(s,s+sum,cmp);
  printf("%d\n",sum);
  for (i=0;i<sum;i++)
  {
      if (i==0||s[i].score!=s[i-1].score) s[i].totalrank=i+1;
      else s[i].totalrank = s[i-1].totalrank;
  }
  for (i=0;i<sum;i++)
  {
      printf("%s %d %d %d\n", s[i].id,s[i].totalrank,s[i].kaochanghao,s[i].kaochangrank);
  }
    return 0;
}
```
