A Digital Library contains millions of books, stored according to their titles, authors, key words of their abstracts, publishers, and published years. Each book is assigned an unique 7-digit number as its ID. Given any query from a reader, you are supposed to output the resulting books, sorted in increasing order of their ID's.
### 输入格式
Each input file contains one test case. For each case, the first line contains a positive integer N (≤10<sup>4</sup>) which is the total number of books. Then N blocks follow, each contains the information of a book in 6 lines:
  Line #1: the 7-digit ID number;
  Line #2: the book title -- a string of no more than 80 characters;
  Line #3: the author -- a string of no more than 80 characters;
  Line #4: the key words -- each word is a string of no more than 10 characters without any white space, and the keywords are separated by exactly one space;
  Line #5: the publisher -- a string of no more than 80 characters;
  Line #6: the published year -- a 4-digit number which is in the range [1000, 3000].
It is assumed that each book belongs to one author only, and contains no more than 5 key words; there are no more than 1000 distinct key words in total; and there are no more than 1000 distinct publishers.
After the book information, there is a line containing a positive integer M (≤1000) which is the number of user's search queries. Then M lines follow, each in one of the formats shown below:
  1: a book title
  2: name of an author
  3: a key word
  4: name of a publisher
  5: a 4-digit number representing the year
### 输出格式
For each query, first print the original query in a line, then output the resulting book ID's in increasing order, each occupying a line. If no book is found, print `Not Found` instead.
### 输入样例
```
3
1111111
The Testing Book
Yue Chen
test code debug sort keywords
ZUCS Print
2011
3333333
Another Testing Book
Yue Chen
test code sort keywords
ZUCS Print2
2012
2222222
The Testing Book
CYLL
keywords debug book
ZUCS Print2
2011
6
1: The Testing Book
2: Yue Chen
3: keywords
4: ZUCS Print
5: 2011
3: blablabla
```
### 输出样例
```
1: The Testing Book
1111111
2222222
2: Yue Chen
1111111
3333333
3: keywords
1111111
2222222
3333333
4: ZUCS Print
1111111
5: 2011
1111111
2222222
3: blablabla
Not Found
```

### 题解
```
#输出id一定要%07d,否则最后两组不过。太坑了。。
#include <iostream>
#include <vector>
#include <string>
#include <cstring>
#include <cstdio>
#include <cmath>
#include <algorithm>
#include <map>
#include <set>
using namespace std;
map<string,set<int>>title,auth,keyw,pub,year;
set<int>::iterator it;
int n,i,id;
void tianjia(map<string,set<int>>&s, string t,int id)
{
    s[t].insert(id);
}
void print(string t, map<string,set<int>>&s)
{
    if (s.find(t)==s.end())
        printf("Not Found\n");
    else
    {
        for (it=s[t].begin();it!=s[t].end();it++)
        {
            printf("%d\n",*it);
        }
    }
}
int main()
{
  scanf("%d",&n);
  getchar();
  for (i=0;i<n;i++)
  {
      scanf("%d",&id);
      getchar();
      string ti,ming,key,p,y;
      getline(cin,ti);
      tianjia(title,ti,id);
      getline(cin,ming);
      tianjia(auth,ming,id);
      getline(cin,key);
      while(key.find(" ")!=-1)
      {
          tianjia(keyw,key.substr(0,key.find(" ")),id);
          key = key.substr(key.find(" ")+1);
      }
      tianjia(keyw,key,id);
      getline(cin,p);
      tianjia(pub,p,id);
      getline(cin,y);
      tianjia(year,y,id);
  }
  cin>>n;
  getchar();
  string a;
  for (i=0;i<n;i++)
    {
        getline(cin,a);
        printf("%s\n",a.c_str());
        char b=a[0];
        a=a.substr(a.find(" ")+1);
        if (b=='1')
            print(a,title);
        else if (b=='2')
            print(a,auth);
        else if (b=='3')
            print(a,keyw);
        else if (b=='4')
            print(a,pub);
        else
            print(a,year);
    }
    return 0;
}
```
