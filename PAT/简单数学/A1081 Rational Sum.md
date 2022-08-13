Given N rational numbers in the form numerator/denominator, you are supposed to calculate their sum.
### 输入格式
Each input file contains one test case. Each case starts with a positive integer N (≤100), followed in the next line N rational numbers a1/b1 a2/b2 ... where all the numerators and denominators are in the range of long int. If there is a negative number, then the sign must appear in front of the numerator.
### 输出格式
For each test case, output the sum in the simplest form integer numerator/denominator where integer is the integer part of the sum, numerator < denominator, and the numerator and the denominator have no common factor. You must output only the fractional part if the integer part is 0.
### 输入样例1
```
5
2/5 4/15 1/30 -2/60 8/3
```
### 输出样例1
```
3 1/3
```
### 输入样例2
```
2
4/3 2/3
```
### 输出样例2
```
2
```
### 输入样例3
```
3
1/3 -1/6 1/8
```
### 输出样例3
```
7/24
```

### 题解
```
#include<iostream>
#include<stack>
#include<string>
#include<algorithm>
#include<queue>
#include<vector>
#include<cmath>
 using namespace std;
struct fenshu
{
    long long fenzi;
    long long fenmu;
}fen[105];
long long gcd(long long a, long long b)
{
    if (a<b)
        swap(a,b);
    if (b==0)
        return a;
    else
        return gcd(b,a%b);
}
 int main()
 {
   int n,i,j;
   cin>>n;
   for (i=0;i<n;i++)
   {
       string t;
       bool isminus = false;
       long long tt=0;
       cin>>t;
       for (j=0;j<t.size();j++)
       {
           if (t[j]=='-')
            isminus = true;
           else if (t[j]=='/')
           {
               if (isminus)
                tt = -tt;
               fen[i].fenzi = tt;
               tt=0;
           }
           else
           {
               tt=tt*10+(t[j]-'0');
           }
       }
       fen[i].fenmu=tt;
   }
   for (i=1;i<n;i++)
   {
       fen[0].fenzi = fen[0].fenzi*fen[i].fenmu+fen[0].fenmu*fen[i].fenzi;
       fen[0].fenmu*=fen[i].fenmu;
       long long g = gcd(abs(fen[0].fenzi), abs(fen[0].fenmu));
       fen[0].fenzi/=g;
       fen[0].fenmu/=g;
   }
   if (fen[0].fenzi==0)
       cout<<0<<endl;
   else if (fen[0].fenzi<fen[0].fenmu)
    cout<<fen[0].fenzi<<"/"<<fen[0].fenmu<<endl;
   else
   {
       cout<<fen[0].fenzi/fen[0].fenmu;
       fen[0].fenzi = fen[0].fenzi%fen[0].fenmu;
       if (fen[0].fenzi)
       {
           cout<<" "<<fen[0].fenzi<<"/"<<fen[0].fenmu;
       }
   }
    return 0;
 }
```
