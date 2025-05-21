# C. XOR and Triangle

time limit per test: 2 seconds

memory limit per test: 256 megabytes

input: standard input

output: standard output

This time, the pink soldiers have given you an integer $x$ ($x \ge 2$).

Please determine if there exists a **positive** integer $y$ that satisfies the following conditions.

-   $y$ is **strictly** less than $x$.
-   There exists a **non-degenerate triangle**$^{\text{∗}}$ with side lengths $x$, $y$, $x \oplus y$. Here, $\oplus$ denotes the [bitwise XOR operation](https://en.wikipedia.org/wiki/Bitwise_operation#XOR).

Additionally, if there exists such an integer $y$, output any.

$^{\text{∗}}$A triangle with side lengths $a$, $b$, $c$ is non-degenerate when $a+b &gt; c$, $a+c &gt; b$, $b+c &gt; a$.

## **Input**

Each test contains multiple test cases. The first line contains the number of test cases $t$ ($1 \le t \le 2000$). The description of the test cases follows.

The only line of each test case contains a single integer $x$ ($2 \le x \le 10^9$).

## **Output**

For each test case, print one integer on a separate line. The integer you must output is as follows:

-   If there exists an integer $y$ satisfying the conditions, output the value of $y$ ($1 \le y &lt; x$);
-   Otherwise, output $-1$.

If there exist multiple integers that satisfy the conditions, you may output any.

## Example

### Input

```
7
5
2
6
3
69
4
420
```

### Output

```
3
-1
5
-1
66
-1
320
```

### **Note**

In the first test case, there exists a non-degenerate triangle with side lengths $3$, $5$, and $3 \oplus 5 = 6$. Therefore, $y=3$ is a valid answer.

In the second test case, $1$ is the only possible candidate for $y$, but it cannot make a non-degenerate triangle. Therefore, the answer is $-1$.

## 代码

![5cdbc1c1564804249e8934f8f1201ee7_720](https://gitee.com/chen-houchao/images/raw/master/202503121507011.png)

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;

void solve() {
  int x;
  cin >> x;
  int ans = -1;
  for (int i = 0; i <= 30; i++) {
    for (int j = 0; j <= 30; j++) {
      int y = (1 << i) | (1 << j);
      if (y > x) break;

      // 判断是否能构成三角形
      if (y < x && x + y > (x ^ y) && y + (x ^ y) > x) {
        ans = y;
        cout << ans << endl;
        return;
      }
    }
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

