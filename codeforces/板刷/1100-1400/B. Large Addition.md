# B. Large Addition

time limit per test: 1 second

memory limit per test: 256 megabytes

input: standard input

output: standard output

A digit is large if it is between $5$ and $9$, inclusive. A positive integer is large if all of its digits are large.

You are given an integer $x$. Can it be the sum of two large positive integers with the **same number of digits**?

**Input**

The first line contains a single integer $t$ ($1 \leq t \leq 10^4$) — the number of test cases.

The only line of each test case contains a single integer $x$ ($10 \leq x \leq 10^{18}$).

**Output**

For each test case, output $\texttt{YES}$ if $x$ satisfies the condition, and $\texttt{NO}$ otherwise.

You can output $\texttt{YES}$ and $\texttt{NO}$ in any case (for example, strings $\texttt{yES}$, $\texttt{yes}$, and $\texttt{Yes}$ will be recognized as a positive response).

## Example

### Input

```
11
1337
200
1393938
1434
98765432123456789
11111111111111111
420
1984
10
69
119
```

### Output

```
YES
NO
YES
YES
NO
YES
NO
YES
YES
NO
NO
```

### **Note**

In the first test case, we can have $658 + 679 = 1337$.

In the second test case, it can be shown that no numbers of equal length and only consisting of large digits can add to $200$.

In the third test case, we can have $696\,969 + 696\,969 = 1\,393\,938$.

In the fourth test case, we can have $777 + 657 = 1434$.

## 代码

​	首先，我们判断末位的范围一定在`[0, 8]`之间。因为相加的末位两个数最小的和为`10`（当两个都为`5`时），最大的和为`18`（当两个都为`9`时）。

​	然后判断中间的数的范围在`[1, 9]`之间。和末位一样，但是由于每一位最小的和都为`10`，一定有进位，所以中间的数的范围要在末位的范围的基础上加`1`也就是`[1, 9]`。

​	首位一定是`1`不可能是其他数。考虑第二位的和的范围`[10, 18]`，再加上进位也才是`[11, 19]`，不可能有多的进位，所以首位只能是`1`。

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  string x;
  cin >> x;
  // 首位必须为1，末位不能为9
  if (x[0] != '1' || x.back() == '9') {
    cout << "NO" << endl;
    return;
  }
  // 中间不能有0
  for (int i = 1; i < x.size() - 1; i++) {
    if (x[i] == '0') {
      cout << "NO" << endl;
      return;
    }
  }
  // 如果都满足，那么输出YES
  cout << "YES" << endl;
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

