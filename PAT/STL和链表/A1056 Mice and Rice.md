Mice and Rice is the name of a programming contest in which each programmer must write a piece of code to control the movements of a mouse in a given map. The goal of each mouse is to eat as much rice as possible in order to become a FatMouse.
First the playing order is randomly decided for N<sub>P</sub> programmers. Then every N<sub>G</sub> programmers are grouped in a match. The fattest mouse in a group wins and enters the next turn. All the losers in this turn are ranked the same. Every N<sub>G</sub> winners are then grouped in the next match until a final winner is determined.
For the sake of simplicity, assume that the weight of each mouse is fixed once the programmer submits his/her code. Given the weights of all the mice and the initial playing order, you are supposed to output the ranks for the programmers.
### 输入格式
Each input file contains one test case. For each case, the first line contains 2 positive integers: N<sub>P</sub> and N<sub>G</sub>(≤1000), the number of programmers and the maximum number of mice in a group, respectively. If there are less than N<sub>G</sub> mice at the end of the player's list, then all the mice left will be put into the last group. The second line contains N<sub>P</sub> distinct non-negative numbers W<sub>i</sub>(i=0,⋯,N<sub>P</sub>−1) where each W<sub>i</sub> is the weight of the i-th mouse respectively. The third line gives the initial playing order which is a permutation of 0,⋯,N<sub>P</sub>−1 (assume that the programmers are numbered from 0 to N<sub>P</sub>−1). All the numbers in a line are separated by a space.
### 输出格式
For each test case, print the final ranks in a line. The i-th number is the rank of the i-th programmer, and all the numbers must be separated by a space, with no extra space at the end of the line.
### 输入样例
```
11 3
25 18 0 46 37 3 19 22 57 56 10
6 0 8 7 10 5 9 1 4 2 3
```
### 输出样例
```
5 5 5 2 5 5 5 3 1 3 5
```

### 题解
```
#include <iostream>
#include <vector>
#include <string>
#include <cstring>
#include <cstdio>
#include <cmath>
#include <algorithm>
#include <map>
#include <vector>
using namespace std;
vector<int>ran[1005];
vector<int>::iterator it;
struct mouse
{
    int id;
    int weight;
    int ran;
    bool flag;
}mice[1005];
int main()
{
    int m,n,i;
    cin>>m>>n;
    for(i=0;i<m;i++)
    {
        mice[i].id=i;
        mice[i].ran=-1;
        mice[i].flag=true;
        cin>>mice[i].weight;
    }
    for(i=0;i<m;i++)
    {
        int t;
        cin>>t;
        ran[0].push_back(t);
    }
    int now=0;
    while(ran[now].size()>1)
    {
        int t=0,noww=-1,nowi;
        for(it=ran[now].begin();it!=ran[now].end();it++)
        {
            if (t<n)
            {
                t++;
                if (mice[*it].weight>noww)
                {
                    noww=mice[*it].weight;
                    nowi=mice[*it].id;
                }
            }
            else
            {
                t=0;
                ran[now+1].push_back(nowi);
                it--;
                noww=-1;
            }
        }
        if (t)
            ran[now+1].push_back(nowi);
        now++;
    }
    int r=1;
    while(now>=0)
    {
        int t=0;
        for(it=ran[now].begin();it!=ran[now].end();it++)
        {

            if (mice[*it].flag)
            {
                t++;
                mice[*it].ran=r;
                mice[*it].flag=false;
            }
        }
        r+=t;
        now--;
    }
    for (i=0;i<m;i++)
    {
        cout<<mice[i].ran;
        if (i!=m-1)
            cout<<" ";
    }
    return 0;
}
```
