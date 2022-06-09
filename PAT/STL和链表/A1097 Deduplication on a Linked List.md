Given a singly linked list L with integer keys, you are supposed to remove the nodes with duplicated absolute values of the keys. That is, for each value K, only the first node of which the value or absolute value of its key equals K will be kept. At the mean time, all the removed nodes must be kept in a separate list. For example, given L being 21→-15→-15→-7→15, you must output 21→-15→-7, and the removed list -15→15.
### 输入格式
Each input file contains one test case. For each case, the first line contains the address of the first node, and a positive N (≤10<sup>5</sup>) which is the total number of nodes. The address of a node is a 5-digit nonnegative integer, and NULL is represented by −1.
Then N lines follow, each describes a node in the format:
```
Address Key Next
```
where `Address` is the position of the node, `Key` is an integer of which absolute value is no more than 10<sup>4</sup>, and `Next` is the position of the next node.
### 输出格式
For each case, output the resulting linked list first, then the removed list. Each node occupies a line, and is printed in the same format as in the input.
### 输入样例
```
00100 5
99999 -7 87654
23854 -15 00000
87654 15 -1
00000 -15 99999
00100 21 23854
```
### 输出样例
```
00100 21 23854
23854 -15 99999
99999 -7 -1
00000 -15 87654
87654 15 -1
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
#include <vector>
using namespace std;
struct no
{
    int address;
    int data;
    int tdata;
    int next;
    bool operator <(const no p)
    {
        return data>p.data;
    }
}nodes[100010],tnodes[100010],fnodes[100010];
bool flag[10010];
int main()
{
   fill(flag,flag+10010,true);
   int s,i,n,t=0,f=0;
   cin>>s>>n;
   for (i=0;i<n;i++)
   {
       int ad;
       cin>>ad;
       nodes[ad].address=ad;
       cin>>nodes[ad].data>>nodes[ad].next;
       nodes[ad].tdata=abs(nodes[ad].data);
   }
   while(s!=-1)
   {
       if(flag[nodes[s].tdata])
       {
           flag[nodes[s].tdata]=false;
           tnodes[t++]=nodes[s];
       }
       else
           fnodes[f++]=nodes[s];
       s=nodes[s].next;
   }
   for(i=0;i<t;i++)
   {
       if (i!=t-1)
        printf("%05d %d %05d\n",tnodes[i].address,tnodes[i].data,tnodes[i+1].address);
       else
        printf("%05d %d -1\n",tnodes[i].address,tnodes[i].data);
   }
   for(i=0;i<f;i++)
   {
       if (i!=f-1)
        printf("%05d %d %05d\n",fnodes[i].address,fnodes[i].data,fnodes[i+1].address);
       else
        printf("%05d %d -1\n",fnodes[i].address,fnodes[i].data);
   }
    return 0;
}
```
