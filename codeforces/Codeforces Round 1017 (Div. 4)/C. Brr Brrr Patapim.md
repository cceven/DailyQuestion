# [C. Brr Brrr Patapim](https://codeforces.com/contest/2094/problem/C)

time limit per test: 2 seconds

memory limit per test: 256 megabytes

input: standard input

output: standard output

Brr Brrr Patapim is trying to learn of Tiramisù's secret passcode, which is a permutation$^{\text{∗}}$ of $2\cdot n$ elements. To help Patapim guess, Tiramisù gave him an $n\times n$ grid $G$, in which $G_{i,j}$ (or the element in the $i$\-th row and $j$\-th column of the grid) contains $p_{i+j}$, or the $(i+j)$\-th element in the permutation.

Given this grid, please help Patapim crack the forgotten code. It is guaranteed that the permutation exists, and it can be shown that the permutation can be determined uniquely.

$^{\text{∗}}$A permutation of $m$ integers is a sequence of $m$ integers which contains each of $1,2,\ldots,m$ exactly once. For example, $[1, 3, 2]$ and $[2, 1]$ are permutations, while $[1, 2, 4]$ and $[1, 3, 2, 3]$ are not.

## **Input**

The first line contains an integer $t$ — the number of test cases ($1 \leq t \leq 200$).

The first line of each test case contains an integer $n$ ($1 \leq n \leq 800$).

Each of the following $n$ lines contains $n$ integers, giving the grid $G$. The first of these lines contains $G_{1,1}, G_{1,2},\ldots,G_{1,n}$; the second of these lines contains $G_{2,1}, G_{2,2},\ldots,G_{2,n}$, and so on. ($1 \leq G_{i,j} \leq 2\cdot n$).

It is guaranteed that the grid encodes a valid permutation, and the sum of $n$ over all test cases does not exceed $800$.

## **Output**

For each test case, please output $2n$ numbers on a new line: $p_1,p_2,\ldots,p_{2n}$.

## Example

### Input

```
3
3
1 6 2
6 2 4
2 4 3
1
1
2
2 3
3 4
```

### Output

```
5 1 6 2 4 3 
2 1 
1 2 3 4 
```

## 代码

```cpp
#include <bits/stdc++.h>
using namespace std;

int G[801][801];

void solve() {
  int n;
  cin >> n;
  vector<int> ans(2 * n + 1);
  unordered_set<int> no_used;  // 存储未使用的数，也是最后答案的第一个数
  for (int i = 1; i <= 2 * n; i++) {
    no_used.insert(i);
  }

  for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n; j++) {
      cin >> G[i][j];
      ans[i + j] = G[i][j];
      no_used.erase(ans[i + j]);  // 已经使用
    }
  }

  cout << *no_used.begin() << " ";
  for (int i = 2; i <= 2 * n; i++) {
    cout << ans[i] << " ";
  }
  cout << endl;
}

int main() {
  int t = 1;
  cin >> t;
  while (t--) {
    solve();
  }
  return 0;
}
```

