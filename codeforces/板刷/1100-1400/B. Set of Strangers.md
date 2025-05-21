# B. Set of Strangers

time limit per test: 2 seconds

memory limit per test: 256 megabytes

input: standard input

output: standard output

You are given a table of $n$ rows and $m$ columns. Initially, the cell at the $i$\-th row and the $j$\-th column has color $a_{i, j}$.

Let's say that two cells are strangers if they **don't** share a side. Strangers are allowed to touch with corners.

Let's say that the set of cells is a set of strangers if all pairs of cells in the set are strangers. Sets with no more than one cell are sets of strangers by definition.

In one step, you can choose any set of strangers **such that all cells in it have the same color** and paint all of them in some other color. You can choose the resulting color.

What is the minimum number of steps you need to make the whole table the same color?

## **Input**

The first line contains a single integer $t$ ($1 \le t \le 10^4$) — the number of test cases. Next, $t$ cases follow.

The first line of each test case contains two integers $n$ and $m$ ($1 \le n \le m \le 700$) — the number of rows and columns in the table.

The next $n$ lines contain the colors of cells in the corresponding row $a_{i, 1}, \dots, a_{i, m}$ ($1 \le a_{i, j} \le nm$).

It's guaranteed that the total sum of $nm$ doesn't exceed $5 \cdot 10^5$ over all test cases.

## **Output**

For each test case, print one integer — the minimum number of steps to paint all cells of the table the same color.

## Example

### Input

```
4
1 1
1
3 3
1 2 1
2 3 2
1 3 1
1 6
5 4 5 4 4 5
3 4
1 4 2 2
1 4 3 5
6 6 3 5
```

### Output

```
0
2
1
10
```

### **Note**

In the first test case, the table is painted in one color from the start.

In the second test case, you can, for example, choose all cells with color $1$ and paint them in $3$. Then choose all cells with color $2$ and also paint them in $3$.

In the third test case, you can choose all cells with color $5$ and paint them in color $4$.

## 代码

​	这道题需要将所有不同的颜色变为相同的颜色，但是每次只能操作不相邻的相同的颜色。于是我们可以得到，如果某一种颜色不存在相邻的，那么直接进行一次操作就可以达成目的。如果某一种颜色存在相邻的，那么需要操作两次才能完成转换（首先将不相邻的部分进行转换，然后再转换剩下的部分）。

​	综上所述，我们直接统计总共有多少种颜色，有多少种存在冲突的颜色，然后直接输出结果就可以了。

​	需要注意的是，当不存在冲突的颜色的时候结果需要减去1（目的颜色不需要进行操作）。如果存在冲突的颜色，那么结果需要减去2（将一种冲突的颜色设定为目标颜色，这样可以减少两次操作）

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  int n, m;
  cin >> n >> m;
  // 存储方格颜色
  unordered_set<int> diff_colors;  // 存储颜色种类
  vector<vector<int>> colors(n, vector<int>(m));
  for (int i = 0; i < n; i++) {
    for (int j = 0; j < m; j++) {
      cin >> colors[i][j];
      diff_colors.insert(colors[i][j]);
    }
  }

  unordered_set<int> bad_colors;  // 存在相邻的颜色数
  for (int i = 0; i < n; i++) {
    for (int j = 0; j < m; j++) {
      // 看看与右边的颜色是否相同
      if (i + 1 < n && colors[i][j] == colors[i + 1][j])
        bad_colors.insert(colors[i][j]);
      // 看看与下方的颜色是否相同
      if (j + 1 < m && colors[i][j] == colors[i][j + 1])
        bad_colors.insert(colors[i][j]);
      // 这里不用判断左边和上边，是因为遍历就是自左向右，自上至下
    }
  }

  // 输出答案
  if (bad_colors.empty()) {
    // 如果没有冲突的颜色，那么直接输出不同颜色的种类-1（每种颜色只需要操作一次）
    cout << diff_colors.size() - 1 << endl;
  } else {
    // 如果存在冲突的颜色，那么首先所有的颜色操作一次（diff_colors.size()）
    // 然后冲突的颜色再操作一次（bad_colors.size()）
    // 最后减去两次（将目标颜色定为冲突的一对颜色而不是不冲突的颜色，可以减少两次操作）
    cout << diff_colors.size() + bad_colors.size() - 2 << endl;
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

