# B. The Third Side

time limit per test: 2 seconds

memory limit per test: 256 megabytes

input: standard input

output: standard output

The pink soldiers have given you a sequence $a$ consisting of $n$ positive integers.

You must repeatedly perform the following operation **until there is only $1$ element left**.

-   Choose two **distinct** indices $i$ and $j$.
-   Then, choose a positive integer value $x$ such that there exists a **non-degenerate triangle**$^{\text{∗}}$ with side lengths $a_i$, $a_j$, and $x$.
-   Finally, remove two elements $a_i$ and $a_j$, and append $x$ to the end of $a$.

Please find the maximum possible value of the only last element in the sequence $a$.

$^{\text{∗}}$A triangle with side lengths $a$, $b$, $c$ is non-degenerate when $a+b &gt; c$, $a+c &gt; b$, $b+c &gt; a$.

## **Input**

Each test contains multiple test cases. The first line contains the number of test cases $t$ ($1 \le t \le 10^4$). The description of the test cases follows.

The first line of each test case contains a single integer $n$ ($1 \le n \le 2 \cdot 10^5$).

The second line of each test case contains $n$ integers $a_1,a_2,\ldots,a_n$ ($1 \le a_i \le 1000$) — the elements of the sequence $a$.

It is guaranteed that the sum of $n$ over all test cases does not exceed $2 \cdot 10^5$.

## **Output**

For each test case, output the maximum possible value of the only last element on a separate line.

## Example

### Input

```
4
1
10
3
998 244 353
5
1 2 3 4 5
9
9 9 8 2 4 4 3 5 3
```

### Output

```
10
1593
11
39
```

### **Note**

On the first test case, there is already only one element. The value of the only last element is $10$.

On the second test case, $a$ is initially $[998,244,353]$. The following series of operations is valid:

1.  Erase $a_2=244$ and $a_3=353$, and append $596$ to the end of $a$. $a$ is now $[998,596]$.
2.  Erase $a_1=998$ and $a_2=596$, and append $1593$ to the end of $a$. $a$ is now $[1593]$.

It can be shown that the only last element cannot be greater than $1593$. Therefore, the answer is $1593$.

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;

void solve() {
  int n;  // 数组长度
  cin >> n;
  vector<int> nums(n);
  for (int i = 0; i < n; i++) {
    cin >> nums[i];
  }
  int ans = accumulate(nums.begin(), nums.end(), 0) - (n - 1);
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

