# D. Subtract Min Sort

time limit per test: 2 seconds

memory limit per test: 256 megabytes

input: standard input

output: standard output

You are given a sequence $a$ consisting of $n$ positive integers.

You can perform the following operation any number of times.

-   Select an index $i$ ($1 \le i &lt; n$), and subtract $\min(a_i,a_{i+1})$ from both $a_i$ and $a_{i+1}$.

Determine if it is possible to make the sequence **non-decreasing** by using the operation any number of times.

## **Input**

Each test contains multiple test cases. The first line contains the number of test cases $t$ ($1 \le t \le 10^4$). The description of the test cases follows.

The first line of each test case contains a single integer $n$ ($2 \le n \le 2 \cdot 10^5$).

The second line of each test case contains $a_1,a_2,\ldots,a_n$ ($1 \le a_i \le 10^9$).

It is guaranteed that the sum of $n$ over all test cases does not exceed $2 \cdot 10^5$.

## **Output**

If it is possible to make the sequence **non-decreasing**, print "YES" on a new line. Otherwise, print "NO" on a new line.

You can output the answer in any case. For example, the strings "yEs", "yes", and "Yes" will also be recognized as positive responses.

## Example

### Input

```
5
5
1 2 3 4 5
4
4 3 2 1
4
4 5 2 3
8
4 5 4 5 4 5 4 5
9
9 9 8 2 4 4 3 5 3
```

### Output

```
YES
NO
YES
YES
NO
```

### **Note**

In the first test case, the array is already sorted.

In the second test case, we can show that it is impossible.

In the third test case, after performing an operation on $i=1$, the array becomes $[0,1,2,3]$, which is now in nondecreasing order.

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;

void solve() {
  int n;
  cin >> n;
  vector<int> nums(n);  // 总共有n个数字
  for (int i = 0; i < n; i++) cin >> nums[i];
  // 开始进行判断
  for (int i = 0; i < n - 1; i++) {
    if (nums[i] > nums[i + 1]) {
      cout << "NO" << endl;
      return;
    }

    nums[i + 1] -= nums[i];
  }
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

