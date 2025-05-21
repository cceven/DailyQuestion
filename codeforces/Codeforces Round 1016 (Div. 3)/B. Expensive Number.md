# B. Expensive Number

time limit per test: 1 second

memory limit per test: 256 megabytes

input: standard input

output: standard output

The cost of a positive integer $n$ is defined as the result of dividing the number $n$ by the sum of its digits.

For example, the cost of the number $104$ is $\frac{104}{1 + 0 + 4} = 20.8$, and the cost of the number $111$ is $\frac{111}{1 + 1 + 1} = 37$.

You are given a positive integer $n$ that does not contain leading zeros. You can remove any number of digits from the number $n$ (including none) so that the remaining number contains at least one digit and **is strictly greater than zero**. The remaining digits **cannot** be rearranged. As a result, you **may** end up with a number that has leading zeros.

For example, you are given the number $103554$. If you decide to remove the digits $1$, $4$, and one digit $5$, you will end up with the number $035$, whose cost is $\frac{035}{0 + 3 + 5} = 4.375$.

What is the minimum number of digits you need to remove from the number so that its cost becomes the minimum possible?

## **Input**

The first line contains an integer $t$ ($1 \leq t \leq 1000$) — the number of test cases.

The only line of each test case contains a positive integer $n$ ($1 \leq n \lt 10^{100}$) without leading zeros.

## **Output**

For each test case, output one integer on a new line — the number of digits that need to be removed from the number so that its cost becomes minimal.

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int ll

void solve() {
  string n;
  cin >> n;
  // 统计最后一个非0数后面有多少个0，总共有多少个非0数
  int zero_num = 0, not_zero_num = 0;
  // 从后向前遍历
  for (auto it = n.rbegin(); it != n.rend(); it++) {
    int cur_num = *it - '0';  // 得到当前的数
    if (cur_num >= 1 && cur_num <= 9) {
      // 统计非0数
      not_zero_num++;
    } else if (not_zero_num == 0) {
      // 统计最后一个非0数后面的0
      zero_num++;
    }
  }
  // 去除掉最后一个非0数前面的非0数，以及其后面的0
  int ans = not_zero_num - 1 + zero_num;
  cout << ans << endl;
}

signed main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);
  int t = 1;
  cin >> t;
  while (t--) solve();
  return 0;
}
```

