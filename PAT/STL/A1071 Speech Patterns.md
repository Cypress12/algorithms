People often have a preference among synonyms of the same word. For example, some may prefer "the police", while others may prefer "the cops". Analyzing such patterns can help to narrow down a speaker's identity, which is useful when validating, for example, whether it's still the same person behind an online avatar.
Now given a paragraph of text sampled from someone's speech, can you find the person's most commonly used word?
### 输入格式
Each input file contains one test case. For each case, there is one line of text no more than 1048576 characters in length, terminated by a carriage return`\n`. The input contains at least one alphanumerical character, i.e., one character from the set [`0-9 A-Z a-z`].
### 输出格式
For each test case, print in one line the most commonly occurring word in the input text, followed by a space and the number of times it has occurred in the input. If there are more than one such words, print the lexicographically smallest one. The word should be printed in all lower case. Here a "word" is defined as a continuous sequence of alphanumerical characters separated by non-alphanumerical characters or the line beginning/end.
Note that words are case insensitive.
### 输入样例
```
Can1: "Can a can can a can?  It can!"
```
### 输出样例
```
can 5
```

### 题解
```
#include <iostream>
#include <vector>
#include <string>
#include <cstdio>
#include <cmath>
#include <algorithm>
#include <map>
using namespace std;
map<string,int>a;
map<string,int>::iterator it;
int main()
{
   string s;
   getline(cin,s);
   int i;
   string t="";
   for (i=0;i<s.length();i++)
   {
       if (s[i]>='A'&&s[i]<='Z')
        s[i]=s[i]-'A'+'a';
       if ((s[i]>='a'&&s[i]<='z')||(s[i]>='0'&&s[i]<='9'))
        t+=s[i];
       else
       {
           if (t.length())
            {
                if (a.find(t)!=a.end())
                    a[t]++;
                else
                    a[t]=1;
                t.clear();
            }
       }
   }
   if (t.length())
    {
        if (a.find(t)!=a.end())
            a[t]++;
        else
            a[t]=1;
        t.clear();
    }
   int sum=-1;
   for (it=a.begin();it!=a.end();it++)
   {
       if (it->second>sum)
        {
            sum=it->second;
            s=it->first;
        }
   }
   cout<<s<<" "<<sum;
    return 0;
}
```
