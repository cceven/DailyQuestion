# A. Final Verdict

time limit per test: 1 second

memory limit per test: 256 megabytes

input: standard input

output: standard output

You are given an array $a$ of length $n$, and must perform the following operation until the length of $a$ becomes $1$.

Choose a positive integer $k <|a|$ such that $\frac{|a|}{k}$ is an integer. Split $a$ into $k$ subsequences$^{\text{∗}}$ $s_1, s_2, \ldots, s_k$ such that:

-   Each element of $a$ belongs to exactly one subsequence.
-   The length of every subsequence is equal.

After this, replace $a = \left[ \operatorname{avg}(s_1), \operatorname{avg}(s_2), \ldots, \operatorname{avg}(s_k) \right] $ , where $\operatorname{avg}(s) = \frac{\sum_{i = 1}^{|s|} s_i}{|s|}$ is the average of all the values in the subsequence. For example, $\operatorname{avg}([1, 2, 1, 1]) = \frac{5}{4} = 1.25$.

Your task is to determine whether there exists a sequence of operations such that after all operations, $a = [x]$.

$^{\text{∗}}$A sequence $x$ is a subsequence of a sequence $y$ if $x$ can be obtained from $y$ by the deletion of several (possibly, zero or all) elements.

## **Input**

Each test contains multiple test cases. The first line contains the number of test cases $t$ ($1 \le t \le 500$). The description of the test cases follows.

The first line of each test case contains two integers $n$, $x$ ($1 \leq n, x \leq 100$) — the length of the array $a$ and the final desired value.

The second line contains $n$ integers $a_1, a_2, \ldots, a_n$ ($1 \leq a_i \leq 100$) — the array $a$.

## **Output**

For each test case, output "YES'" (without quotes) if there exists such a sequence of operations, and "NO" (without quotes) otherwise.

You can output "YES" and "NO" in any case (for example, strings "yES", "yes" and "Yes" will be recognized as a positive response).

## Example

### Input

```
4
1 3
3
4 9
7 11 2 5
6 9
1 9 14 12 10 8
10 10
10 10 10 10 10 10 10 10 10 10
```

### Output

```
YES
NO
YES
YES
```

### **Note**

In the first test case, $x = 3$ and $a = [3]$ already holds.

In the second test case, $x = 9$, and there exists no sequence of operations such that after all operations, $a = [9]$.

In the third test case, $x = 9$, and here is one possible sequence of operations.

1.  $k = 2$, $s_1 = [1, 12, 8]$ and $s_2 = [9, 14, 10]$. Hence, $a = [\operatorname{avg}(s_1), \operatorname{avg}(s_2)] = [7, 11]$.
2.  $k = 1$ and $s_1 = [7, 11]$. Hence, $a = [\operatorname{avg}(s_1)] = [9]$.

In the fourth test case, $x = 10$, and here is one possible sequence of operations.

1.  $k = 1$ and $s_1 = [10, 10, 10, 10, 10, 10, 10, 10, 10, 10]$. Hence, $a = [\operatorname{avg}(s_1)] = [10]$.

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;

void solve() {
  int n, x;
  cin >> n >> x;
  int sum = 0;
  for (int i = 0; i < n; i++) {
    int temp;
    cin >> temp;
    sum += temp;
  }
  cout << ((double)sum / n == x ? "YES" : "NO") << endl;
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

