# C. Remove the Ends

time limit per test: 3 seconds

memory limit per test: 256 megabytes

input: standard input

output: standard output

You have an array $a$ of length $n$ consisting of **non-zero** integers. Initially, you have $0$ coins, and you will do the following until $a$ is empty:

-   Let $m$ be the current size of $a$. Select an integer $i$ where $1 \le i \le m$, gain $|a_i|$$^{\text{∗}}$ coins, and then:
    -   if $a_i \lt 0$, then replace $a$ with $[a_1,a_2,\ldots,a_{i - 1}]$ (that is, delete the suffix beginning with $a_i$);
    -   otherwise, replace $a$ with $[a_{i + 1},a_{i + 2},\ldots,a_m]$ (that is, delete the prefix ending with $a_i$).

Find the maximum number of coins you can have at the end of the process.

$^{\text{∗}}$Here $|a_i|$ represents the absolute value of $a_i$: it equals $a_i$ when $a_i \gt 0$ and $-a_i$ when $a_i \lt 0$.

## **Input**

The first line contains an integer $t$ ($1 \le t \le 10^4$) — the number of testcases.

The first line of each testcase contains an integer $n$ ($1 \le n \le 2 \cdot 10^5$) — the length of $a$.

The second line of each testcase contains $n$ integers $a_1,a_2,\ldots,a_n$ ($-10^9 \le a_i \le 10^9$, $a_i \ne 0$).

The sum of $n$ across all testcases does not exceed $2 \cdot 10^5$.

## **Output**

For each test case, output the maximum number of coins you can have at the end of the process.

## Example

### Input

```
3
6
3 1 4 -1 -5 -9
6
-10 -3 -17 1 19 20
1
1
```

### Output

```
23
40
1
```

### **Note**

An example of how to get $23$ coins in the first testcase is as follows:

-   $a = [3, 1, 4, -1, -5, \color{red}{-9}] \xrightarrow{i = 6} a = [3, 1, 4, -1, -5] $ , and get $9$ coins.
-   $a = [\color{red}{3}, 1, 4, -1, -5] \xrightarrow{i = 1} a = [1, 4, -1, -5] $ , and get $3$ coins.
-   $a = [\color{red}{1}, 4, -1, -5] \xrightarrow{i = 1} a = [4, -1, -5] $ , and get $1$ coin.
-   $a = [4, -1, \color{red}{-5}] \xrightarrow{i = 3} a = [4, -1] $ , and get $5$ coins.
-   $a = [4, \color{red}{-1}] \xrightarrow{i = 2} a = [4] $ , and get $1$ coin.
-   $a = [\color{red}{4}] \xrightarrow{i = 1} a = [] $ , and get $4$ coins.

After all the operations, you have $23$ coins.

An example of how to get $40$ coins in the second testcase is as follows:

-   $a = [-10, -3, -17, \color{red}{1}, 19, 20] \xrightarrow{i = 4} a = [19, 20] $ , and get $1$ coin.
-   $a = [\color{red}{19}, 20] \xrightarrow{i = 1} a = [20] $ , and get $19$ coins.
-   $a = [\color{red}{20}] \xrightarrow{i = 1} a = [] $ , and get $20$ coins.

After all the operations, you have $40$ coins.

## 代码

​	如果选择一个正数，那么接下来就需要遍历这个正数的右边舍弃掉左边。如果选择一个负数，那么接下来就需要遍历这个负数的左边舍弃右边。

​	现在假如我们选择了一个数，那么可以发现这个数可以从两个方向，一直遍历左边的正数或者一直遍历右边的负数来到达，所以我们就可以记录每个数的正数前缀和和负数的后缀和，来寻找最大值。

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  int n;
  cin >> n;
  vector<ll> a(n);
  for (auto &x : a) cin >> x;
  vector<ll> pre(n, 0), suf(n, 0);
  // 先处理正数与前缀
  if (a[0] > 0) pre[0] = a[0];
  for (int i = 1; i < n; i++) {
    pre[i] = pre[i - 1];
    if (a[i] > 0) pre[i] += a[i];
  }
  // 然后开始处理负数与后缀
  if (a.back() < 0) suf[n - 1] = abs(a.back());
  for (int i = n - 2; i >= 0; i--) {
    suf[i] = suf[i + 1];
    if (a[i] < 0) suf[i] += abs(a[i]);
  }
  // 开始寻找答案
  ll ans = 0;
  for (int i = 0; i < n; i++) {
    ans = max(ans, pre[i] + suf[i]);
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

