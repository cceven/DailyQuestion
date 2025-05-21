# D. Counting Points

time limit per test: 2 seconds

memory limit per test: 256 megabytes

input: standard input

output: standard output

The pink soldiers drew $n$ circles with their center **on the $x$\-axis** of the plane. Also, they have told that **the sum of radii is exactly $m$**$^{\text{∗}}$.

Please find the number of integer points **inside or on the border of** at least one circle. Formally, the problem is defined as follows.

You are given an integer sequence $x_1,x_2,\ldots,x_n$ and a positive integer sequence $r_1,r_2,\ldots,r_n$, where it is known that $\sum_{i=1}^n r_i = m$.

You must count the number of integer pairs $(x,y)$ that satisfy the following condition.

-   There exists an index $i$ such that $(x-x_i)^2 + y^2 \le r_i^2$ ($1 \le i \le n$).

$^{\text{∗}}$Is this information really useful? Don't ask me; I don't really know.

## **Input**

Each test contains multiple test cases. The first line contains the number of test cases $t$ ($1 \le t \le 10^4$). The description of the test cases follows.

The first line of each test case contains two integers $n$ and $m$ ($1 \le n \le m \le 2\cdot 10^5$).

The second line of each test case contains $x_1,x_2,\ldots,x_n$ — the centers of the circles ($-10^9 \le x_i \le 10^9$).

The third line of each test case contains $r_1,r_2,\ldots,r_n$ — the radii of the circles ($1 \le r_i$, $\sum_{i=1}^n r_i = m$).

It is guaranteed that **the sum of $m$ over all test cases** does not exceed $2\cdot 10^5$.

## **Output**

For each test case, output the number of integer points satisfying the condition on a separate line.

## Example

### Input

```
4
2 3
0 0
1 2
2 3
0 2
1 2
3 3
0 2 5
1 1 1
4 8
0 5 10 15
2 2 2 2
```

## Output

### Copy

```
13
16
14
52
```

### **Note**

On the first test case, the circle with $r_1=1$ is completely inside the circle with $r_2=2$. Therefore, you only have to count the number of integer points inside the latter. There are $13$ integer points such that $x^2+y^2 \le 2^2$, so the answer is $13$.

On the second test case, the circle with $r_1=1$ is not completely inside the circle with $r_2=2$. There are $3$ additional points that are inside the first circle but not inside the second circle, so the answer is $3+13=16$.

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;

void solve() {
  int n, m;
  cin >> n >> m;
  vector<ll> x(n), r(n);
  // 输入x轴坐标和半径
  for (int i = 0; i < n; i++) cin >> x[i];
  for (int i = 0; i < n; i++) cin >> r[i];

  unordered_map<ll, ll> cnt;  // 记录每个x对应的点的数量
  for (int i = 0; i < n; i++) {
    for (int j = x[i] - r[i]; j <= x[i] + r[i]; j++) {
      // 更新当前x对应的点的最大数量
      cnt[j] =
              max(cnt[j],
                  2 * (ll)sqrt(r[i] * r[i] - (j - x[i]) * (j - x[i])) + 1);
    }
  }

  ll ans = 0;
  for (auto &c : cnt) {
    ans += c.second;  // 存储每个x点对应的点的数量
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

