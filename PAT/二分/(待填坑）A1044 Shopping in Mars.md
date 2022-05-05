给出一个数字序列与一个数S，在数字序列中求出所有和值为S的连续子序列（区间下标左端点小的先输出，左端点相同时右端点小的先输出）。若没有这样的序列，求出和值恰好大于S的子序列（即在所有和值大于S的子序列中和值最接近S）。假设下标从1开始
### 输入格式
Each input file contains one test case. For each case, the first line contains 2 numbers: N (≤10<sup>5</sup>), the total number of diamonds on the chain, and M (≤10<sup>8</sup>), the amount that the customer has to pay. Then the next line contains N positive numbers D<sub>1</sub>⋯D<sub>N</sub>(D<sub>i</sub>≤10<sup>3</sup> for all i=1,⋯,N) which are the values of the diamonds. All the numbers in a line are separated by a space.
### 输出格式
For each test case, print i-j in a line for each pair of i ≤ j such that Di + ... + Dj = M. Note that if there are more than one solution, all the solutions must be printed in increasing order of i.
If there is no solution, output i-j for pairs of i ≤ j such that Di + ... + Dj >M with (Di + ... + Dj −M) minimized. Again all the solutions must be printed in increasing order of i.
It is guaranteed that the total value of diamonds is sufficient to pay the given amount.
### 输入样例1
```
16 15
3 2 1 5 4 6 8 7 16 10 15 11 9 12 14 13
```
### 输出样例1
```
1-5
4-6
7-8
11-11
```
### 输入样例2
```
5 13
2 4 5 7 9
```
### 输出样例2
```
2-4
4-5
```

### 题解
```

```
