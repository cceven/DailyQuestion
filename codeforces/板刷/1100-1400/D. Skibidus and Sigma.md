# D. Skibidus and Sigma

time limit per test: 2 seconds

memory limit per test: 256 megabytes

input: standard input

output: standard output

Let's denote the score of an array $b$ with $k$ elements as $\sum_{i=1}^{k}\left(\sum_{j=1}^ib_j\right)$. In other words, let $S_i$ denote the sum of the first $i$ elements of $b$. Then, the score can be denoted as $S_1+S_2+\ldots+S_k$.

Skibidus is given $n$ arrays $a_1,a_2,\ldots,a_n$, each of which contains $m$ elements. Being the sigma that he is, he would like to concatenate them in **any order** to form a single array containing $n\cdot m$ elements. Please find the maximum possible score Skibidus can achieve with his concatenated array!

Formally, among all possible permutations$^{\text{∗}}$ $p$ of length $n$, output the maximum score of $a_{p_1} + a_{p_2} + \dots + a_{p_n}$, where $+$ represents concatenation$^{\text{†}}$.

$^{\text{∗}}$A permutation of length $n$ contains all integers from $1$ to $n$ exactly once.

$^{\text{†}}$The concatenation of two arrays $c$ and $d$ with lengths $e$ and $f$ respectively (i.e. $c + d$) is $c_1, c_2, \ldots, c_e, d_1, d_2, \ldots d_f$.

## **Input**

The first line contains an integer $t$ ($1 \leq t \leq 10^4$) — the number of test cases.

The first line of each test case contains two integers $n$ and $m$ ($1 \leq n \cdot m \leq 2 \cdot 10^5$) — the number of arrays and the length of each array.

The $i$'th of the next $n$ lines contains $m$ integers $a_{i,1}, a_{i,2}, \ldots, a_{i,m}$ ($1 \leq a_{i,j} \leq 10^6$) — the elements of the $i$'th array.

It is guaranteed that the sum of $n \cdot m$ over all test cases does not exceed $2 \cdot 10^5$.

## **Output**

For each test case, output the maximum score among all possible permutations $p$ on a new line.

## Example

### Input

```
3
2 2
4 4
6 1
3 4
2 2 2 2
3 2 1 2
4 1 2 1
2 3
3 4 5
1 1 9
```

### Output

```
41
162
72
```

### **Note**

For the first test case, there are two possibilities for $p$:

-   $p = [1, 2]$. Then, $a_{p_1} + a_{p_2} = [4, 4, 6, 1]$. Its score is $4+(4+4)+(4+4+6)+(4+4+6+1)=41$.
-   $p = [2, 1]$. Then, $a_{p_1} + a_{p_2} = [6, 1, 4, 4]$. Its score is $6+(6+1)+(6+1+4)+(6+1+4+4)=39$.

The maximum possible score is $41$.

In the second test case, one optimal arrangement of the final concatenated array is $[4,1,2,1,2,2,2,2,3,2,1,2]$. We can calculate that the score is $162$.

## 代码

​	直接将各个数组按照数组和从大到小进行排序然后计算结果。可以举例知道，知道数组大小和更大那么最后得到的结果一定更大。如果两个数组不同但是数组和相同（比如`1 3`和`2 2`)，无论怎么排列结果都是相同的。

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  int n, m;
  cin >> n >> m;
  vector<vector<ll>> nums(n, vector<ll>(m));
  vector<ll> special_sum(n);  // 记录权重和和
  vector<ll> normal_sum(n);   // 记录普通和
  for (int i = 0; i < n; i++) {
    for (int j = 0; j < m; j++) {
      cin >> nums[i][j];
      normal_sum[i] += nums[i][j];             // 记录普通和
      special_sum[i] += (m - j) * nums[i][j];  // 记录权重和
    }
  }

  vector<ll> idx(n);  // 记录下标，按照和的大小进行排序
  iota(idx.begin(), idx.end(), 0);
  sort(idx.begin(), idx.end(), [&](const int &i, const int &j) {
    return normal_sum[i] > normal_sum[j];
  });
  // 开始计算答案
  ll ans = 0;
  for (int i = 0; i < n; i++) {
    ans += special_sum[idx[i]] + (n - i - 1) * m * normal_sum[idx[i]];
  }
  cout << ans << endl;
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);
  int t = 1;
  cin >> t;
  while (t--) solve();
  return 0;
}
```

