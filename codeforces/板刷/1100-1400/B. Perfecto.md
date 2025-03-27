# B. Perfecto

time limit per test: 1.5 seconds

memory limit per test: 256 megabytes

input: standard input

output: standard output

A permutation $p$ of length $n$$^{\text{∗}}$ is perfect if, for each index $i$ ($1 \le i \le n$), it satisfies the following:

-   The sum of the first $i$ elements $p_1 + p_2 + \ldots + p_i$ is **not** a perfect square$^{\text{†}}$.

You would like things to be perfect. Given a positive integer $n$, find a perfect permutation of length $n$, or print $-1$ if none exists.

$^{\text{∗}}$A permutation of length $n$ is an array consisting of $n$ distinct integers from $1$ to $n$ in arbitrary order. For example, $[2,3,1,5,4]$ is a permutation, but $[1,2,2]$ is not a permutation ($2$ appears twice in the array), and $[1,3,4]$ is also not a permutation ($n=3$ but there is $4$ in the array).

$^{\text{†}}$A perfect square is an integer that is the square of an integer, e.g., $9=3^2$ is a perfect square, but $8$ and $14$ are not.

## **Input**

Each test contains multiple test cases. The first line contains the number of test cases $t$ ($1 \le t \le 10^4$). The description of the test cases follows.

The first and only line of each test case contains a single integer $n$ ($1 \le n \le 5 \cdot 10^5$).

It is guaranteed that the sum of $n$ over all test cases does not exceed $10^6$.

## **Output**

For each test case:

-   If no solution exists, print a single integer $-1$.
-   Otherwise, print $n$ integers $p_1,p_2,\ldots,p_n$ — the perfect permutation you find.

If there are multiple solutions, print any of them.

## Example

### Input

```
3
1
4
5
```

### Output

```
-1
2 4 1 3
5 1 4 3 2
```

### **Note**

In the first test case, there is only one permutation with length $n = 1$ that is $p = [1]$, which is not perfect:

-   $p_1 = 1 = x^2$ for $x = 1$.

In the second test case, one possible perfect permutation with length $n = 4$ is $p = [2, 4, 1, 3]$:

-   $p_1 = 2 \neq x^2$;
-   $p_1 + p_2 = 2 + 4 = 6 \neq x^2$;
-   $p_1 + p_2 + p_3 = 2 + 4 + 1 = 7 \neq x^2$;
-   $p_1 + p_2 + p_3 + p_4 = 2 + 4 + 1 + 3 = 10 \neq x^2$.

In the third test case, one possible perfect permutation with length $n = 5$ is $p = [5, 1, 4, 3, 2]$:

-   $p_1 = 5 \neq x^2$;
-   $p_1 + p_2 = 5 + 1 = 6 \neq x^2$;
-   $p_1 + p_2 + p_3 = 5 + 1 + 4 = 10 \neq x^2$;
-   $p_1 + p_2 + p_3 + p_4 = 5 + 1 + 4 + 3 = 13 \neq x^2$;
-   $p_1 + p_2 + p_3 + p_4 + p_5 = 5 + 1 + 4 + 3 + 2 = 15 \neq x^2$.

## 代码

​	首先我们需要判断从`1`到`n`的和是不是一个完全平方数，这决定了有没有解。因为如果`1`到`n`的和为一个完全平方数，那么无论怎么排列，最大的一个数组一定不符合要求。

​	判断完了有没有解后，我们就要开始排列数字。从`1`开始遍历到`n`，并计算当前的累积和。如果当前的和为完全平方数，说明当前的排列不符合要求，那么我们直接交换`i`和`i+1`，那么新得到的累积和就是`完全平方数+1`，可知新得到的数一定不是完全平方数，因为没有两个完全平方数的差为`1`.

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  ll n;
  cin >> n;
  // 首先计算能不能有解，如果所有的数加起来是一个完全平方数，那么一定无解
  ll sum = (1 + n) * n / 2;
  if (sqrt(sum) == (int)sqrt(sum)) {
    cout << "-1" << endl;
    return;
  }

  // 接下来开始从1开始遍历
  vector<ll> ans(n + 1);
  iota(ans.begin(), ans.end(), 0);
  for (int i = 1; i < n; i++) {
    ll cur_sum = (1LL + i) * i / 2;
    // 如果当前到i位的和是一个完全平方数，那么需要交换i和i+1，显然交换后一定不是完全平方数
    if (sqrt(cur_sum) == (int)sqrt(cur_sum)) {
      swap(ans[i], ans[i + 1]);
    }
  }
  // 输出答案
  for (int i = 1; i <= n; i++) {
    cout << ans[i] << " ";
    if (i == n) cout << endl;
  }
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

### 判断一个数字是否是完全平方数

使用`sqrt(num) == (int)sqrt(num)`

因为`sqrt()`函数得到的结果为浮点数，我们使用`int`转换为整数，如果两个相等那么说明`num`是完全平方数