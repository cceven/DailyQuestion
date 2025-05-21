# A. Fibonacciness

time limit per test: 1 second

memory limit per test: 256 megabytes

input: standard input

output: standard output

There is an array of $5$ integers. Initially, you only know $a_1,a_2,a_4,a_5$. You may set $a_3$ to any positive integer, negative integer, or zero. The Fibonacciness of the array is the number of integers $i$ ($1 \leq i \leq 3$) such that $a_{i+2}=a_i+a_{i+1}$. Find the maximum Fibonacciness over all integer values of $a_3$.

## **Input**

The first line contains an integer $t$ ($1 \leq t \leq 500$) — the number of test cases.

The only line of each test case contains four integers $a_1, a_2, a_4, a_5$ ($1 \leq a_i \leq 100$).

## **Output**

For each test case, output the maximum Fibonacciness on a new line.

## Example

### Input

```
6
1 1 3 5
1 3 2 1
8 10 28 100
100 1 100 1
1 100 1 100
100 100 100 100
```

### Output

```
3
2
2
1
1
2
```

### **Note**

In the first test case, we can set $a_3$ to $2$ to achieve the maximal Fibonacciness of $3$.

In the third test case, it can be shown that $2$ is the maximum Fibonacciness that can be achieved. This can be done by setting $a_3$ to $18$.

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;

void solve() {
  int a[6];
  // 首先输入除了a[3]之外的数字
  for (int i = 1; i <= 5; i++) {
    if (i == 3) continue;
    cin >> a[i];
  }

  int max_cnt = 0;
  auto check  = [&](int num) {
    a[3]         = num;
    int curr_cnt = 0;
    for (int i = 1; i <= 3; i++) {
      if (a[i] + a[i + 1] == a[i + 2]) curr_cnt++;
    }
    max_cnt = max(max_cnt, curr_cnt);
  };

  check(a[1] + a[2]);
  check(a[4] - a[2]);
  check(a[5] - a[4]);
  cout << max_cnt << endl;
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);
  int t;
  cin >> t;
  while (t--) solve();
  return 0;
}
```

