给定整数N、K、P，将N表示成K个正整数（可以相同，递减排列）的P次方的和，即N=n<sub>1</sub>^P+...+n<sub>k</sub>^p。如果有多种方案，那么选择底数和最大的方案；如果还有多种方案，那么选择底数序列的字典序最大的方案。如果没有方案输出`Impossible`
### 输入样例1
```
169 5 2
```
### 输出样例1
```
169 = 6^2 + 6^2 + 6^2 + 6^2 + 5^2
```
### 输入样例2
```
169 167 3
```
### 输出样例2
```
Impossible
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
vector<int>num,t,ans;
int n,k,p,i,he=0,ma=0;
void dfs(int index,int nown,int nows,int nowh)
{
    if (nown==k&&nows==n)
    {
        if (nowh>he)
        {
            he=nowh;
            ans=t;
        }
        return;
    }
    if (nown>k||nows>n)
        return;
    if (index-1>=0)
    {
        t.push_back(index);
        dfs(index,nown+1,nows+num[index],nowh+index);
        t.pop_back();
        dfs(index-1,nown,nows,nowh);
    }
}
int main()
{
   cin>>n>>k>>p;
   for(i=0;pow(i,p)<=n;i++)
      num.push_back(pow(i,p));
   dfs(num.size()-1,0,0,0);
   if (ans.size()!=k)
    cout<<"Impossible"<<endl;
   else
   {
       cout<<n<<" = ";
       for (vector<int>::iterator it=ans.begin();it!=ans.end();it++)
       {
           cout<<*it<<"^"<<p;
           if (it!=ans.end()-1)
            cout<<" + ";
       }
   }


    return 0;
}
```
