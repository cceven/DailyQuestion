# **C - Shortest Duplicate Subarray** 

------

Time Limit: 2 sec / Memory Limit: 1024 MB

Score : 300300 points

## Problem Statement

You are given a positive integer $N$ and an integer sequence $A = (A_1,A_2,\dots,A_N)$ of length $N$.

Determine whether there exists a non-empty (contiguous) subarray of $A$ that has a repeated value, occurring multiple times in $A$. If such a subarray exists, find the length of the shortest such subarray.

## Constraints

-   $1 \leq N \leq 2 \times 10^5$
-   $1 \leq A_i \leq 10^6 \ (1 \leq i \leq N)$
-   All input values are integers.

## Input

The input is given from Standard Input in the following format:

```
$N$
$A_1$ $A_2$ $\dots$ $A_N$
```

## Output

If there is no (contiguous) subarray satisfying the condition in the problem statement, print `-1`. Otherwise, print the length of the shortest such subarray.

## Sample Input 1

```
5
3 9 5 3 1
```

## Sample Output 1

```
4
```

$(3,9,5,3)$ and $(3,9,5,3,1)$ satisfy the condition. The shorter one is $(3,9,5,3)$, which has length $4$.

## Sample Input 2

```
4
2 5 3 1
```

## Sample Output 2

```
\-1
```

There is no subarray that satisfies the condition.

## Sample Input 3

```
10
1 1 2 3 5 8 13 21 34 55
```

## Sample Output 3

```
2
```

## 代码

不定滑动窗口求最小值

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;

void solve() {
  int N;
  cin >> N;
  vector<int> A(N);
  for (auto &a : A) {
    cin >> a;
  }

  // 开始检测
  int l = 0, ans = INT_MAX;
  unordered_map<int, int> cnt;
  for (int r = 0; r < N; r++) {
    cnt[A[r]]++;

    while (cnt[A[r]] > 1) {
      ans = min(ans, r - l + 1);
      cnt[A[l]]--;
      l++;
    }
  }
  cout << (ans != INT_MAX ? ans : -1) << endl;
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);

  solve();
  return 0;
}
```

