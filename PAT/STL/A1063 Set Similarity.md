Given two sets of integers, the similarity of the sets is defined to be N<sub>c</sub>/N<sub>t</sub>×100%, where N<sub>c</sub> is the number of distinct common numbers shared by the two sets, and N<sub>t</sub> is the total number of distinct numbers in the two sets. Your job is to calculate the similarity of any given pair of sets.
### 输入格式
Each input file contains one test case. Each case first gives a positive integer N (≤50) which is the total number of sets. Then N lines follow, each gives a set with a positive M (≤10<sup>4</sup>) and followed by M integers in the range [0,10<sup>9</sup>]. After the input of sets, a positive integer K (≤2000) is given, followed by K lines of queries. Each query gives a pair of set numbers (the sets are numbered from 1 to N). All the numbers in a line are separated by a space.
### 输出格式
For each query, print in one line the similarity of the sets, in the percentage form accurate up to 1 decimal place.
### 输入样例
```
3
3 99 87 101
4 87 101 5 87
7 99 101 18 5 135 18 99
2
1 2
1 3
```
### 输出样例
```
50.0%
33.3%
```

### 题解
```
#include <iostream>
#include <vector>
#include <string>
#include <cstdio>
#include <cmath>
#include <algorithm>
#include <set>
using namespace std;
set<int> a[55];
int n,i,j,m;
int main()
{
    scanf("%d",&n);
    for (i=1;i<=n;i++)
    {
        scanf("%d",&m);
        for (j=0;j<m;j++)
        {
            int t;
            scanf("%d",&t);
            a[i].insert(t);
        }
    }
    scanf("%d",&n);
    for (i=0;i<n;i++)
    {
        int c,d;
        scanf("%d %d",&c,&d);
        int jiao=0,bing=0;
        set<int>::iterator it1;
        for (it1=a[c].begin();it1!=a[c].end();it1++)
        {
            if(a[d].find(*it1)!=a[d].end())
                jiao++;
        }
        bing=a[c].size()+a[d].size()-jiao;
        printf("%.1f%%\n",jiao/double(bing)*100);
    }
    return 0;
}
```
