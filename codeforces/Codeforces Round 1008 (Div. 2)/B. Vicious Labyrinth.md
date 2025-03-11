# B. Vicious Labyrinth

time limit per test: 1.5 seconds

memory limit per test: 256 megabytes

input: standard input

output: standard output

There are $n$ cells in a labyrinth, and cell $i$ ($1 \leq i \leq n$) is $n - i$ kilometers away from the exit. In particular, cell $n$ is the exit. Note also that each cell is connected to the exit but is not accessible from any other cell in any way.

In each cell, there is initially exactly one person stuck in it. You want to help everyone get as close to the exit as possible by installing a teleporter in each cell $i$ ($1 \leq i \leq n$), which translocates the person in that cell to another cell $a_i$.

The labyrinth owner caught you in the act. Amused, she let you continue, but under some conditions:

-   Everyone must use the teleporter exactly $k$ times.
-   No teleporter in any cell can lead to the same cell it is in. Formally, $i \neq a_i$ for all $1 \leq i \leq n$.

You must find a teleporter configuration that minimizes the sum of distances of all individuals from the exit after using the teleporter exactly $k$ times while still satisfying the restrictions of the labyrinth owner.

If there are many possible configurations, you can output any of them.

## **Input**

Each test contains multiple test cases. The first line contains the number of test cases $t$ ($1 \le t \le 10^4$). The description of the test cases follows.

The first and only line of each test case contains two integers $n$ and $k$ ($2 \leq n \leq 2 \cdot 10^5$, $1 \leq k \leq 10^9$) — the number of cells in the labyrinth and the value $k$.

It is guaranteed that the total sum of $n$ across all test cases does not exceed $2 \cdot 10^5$.

## **Output**

For each test case, output $n$ integers — the destinations of the teleporters $a_1, a_2, \ldots, a_n$ in order, satisfying the given conditions ($1 \leq a_i \leq n$, $a_i \neq i$).

## Example

### Input

```
2
2 1
3 2
```

### Output

```
2 1
2 3 2
```

### **Note**

In the first test case, the position of each person is as follows.

-   Before teleporting: $[1, 2]$.
-   First teleportation: $[2, 1]$.

The distance sum is $(2-2) + (2-1) = 1$, which is the minimum possible.

In the second test case, the position of each person is as follows.

-   Before teleporting: $[1, 2, 3]$.
-   First teleportation: $[2, 3, 2]$.
-   Second teleportation: $[3, 2, 3]$.

The distance sum is $(3-3) + (3-2) + (3-3) = 1$, which is the minimum possible.

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;

void solve() {
  int n, k;
  cin >> n >> k;

  if (k & 1) {  // k是奇数的情况,除了最后一个节点，其余全部一步到位
    for (int i = 1; i <= n - 1; i++) cout << n << " ";
    cout << n - 1 << endl;
  } else {  // k是偶数的情况，除了倒数第二个节点，所有节点先在倒数第二个节点的位置进行中转
    for (int i = 1; i <= n - 2; i++) {
      cout << n - 1 << " ";
    }
    cout << n << " " << n - 1 << endl;
  }
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

