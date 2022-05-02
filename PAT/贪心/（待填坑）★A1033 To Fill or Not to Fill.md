已知起点和终点的距离为D，油箱的最大容量为Cmax，单位汽油能够支持前进Davg。给定N个加油站的单位油价和离起点的距离，汽车初始时刻处于起点位置，油箱为空，且可以在任意加油站购买任意量汽油（不超过油箱容量），求从起点到终点的最小花费。如果无法到达终点，输出能够行驶的最远距离。Cancel changes
### 输入格式
Each input file contains one test case. For each case, the first line contains 4 positive numbers: Cmax(≤ 100), the maximum capacity of the tank; D (≤30000), the distance between Hangzhou and the destination city; Davg(≤20), the average distance per unit gas that the car can run; and N (≤ 500), the total number of gas stations. Then N lines follow, each contains a pair of non-negative numbers: P<sub>i</sub>, the unit gas price, and D<sub>i</sub>(≤D), the distance between this station and Hangzhou, for i=1,⋯,N. All the numbers in a line are separated by a space.
### 输出格式
For each test case, print the cheapest price in a line, accurate up to 2 decimal places. It is assumed that the tank is empty at the beginning. If it is impossible to reach the destination, print `The maximum travel distance = X` where `X` is the maximum possible distance the car can run, accurate up to 2 decimal places.
### 输入样例1
```
50 1300 12 8
6.00 1250
7.00 600
7.00 150
7.10 0
7.20 200
7.50 400
7.30 1000
6.85 300
```
### 输出样例1
```
749.17
```
### 输入样例2
```
50 1300 12 2
7.10 0
7.00 600
```
### 输出样例2
```
The maximum travel distance = 1200.00
```

### 题解
```

```
