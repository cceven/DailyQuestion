# **D - Pigeon Swap**

------

Time Limit: 2 sec / Memory Limit: 1024 MB

Score : 350350 points

## Problem Statement

There are $N$ pigeons labeled $1, 2, \ldots, N$ and $N$ nests labeled $1, 2, \ldots, N$.

Initially, pigeon $i$ $(1 \leq i \leq N)$ is in nest $i$.

You will perform $Q$ operations on these pigeons.

There are three types of operations:

-   Type $1$: You are given integers $a$ and $b$ $(1 \leq a \leq N, 1 \leq b \leq N)$. Take pigeon $a$ out of its current nest and move it to nest $b$.
-   Type $2$: You are given integers $a$ and $b$ $(1 \leq a &lt; b \leq N)$. Move all pigeons in nest $a$ to nest $b$, and move all pigeons in nest $b$ to nest $a$. These two moves happen simultaneously.
-   Type $3$: You are given an integer $a$ $(1 \leq a \leq N)$. Pigeon $a$ reports the label of the nest it is currently in.

Print the result of each Type $3$ operation in the order the operations are given.

## Constraints

-   $1 \leq N \leq 10^6$
-   $1 \leq Q \leq 3 \times 10^5$
-   Every operation is of Type $1$, $2$, or $3$.
-   All operations are valid according to the problem statement.
-   There is at least one Type $3$ operation.
-   All input values are integers.

## Input

The input is given from Standard Input in the following format:

```
$N$ $Q$
$op _ 1$
$op _ 2$
$\vdots$
$op _ Q$
```

Here, $op _ i$ on the line $i+1$ represents the $i$\-th operation in one of the following formats.

If the $i$\-th operation is of Type $1$, $op _ i$ is in the following format:

```
$1$ $a$ $b$
```

This corresponds to a Type $1$ operation with the given integers being $a$ and $b$.

If the $i$\-th operation is of Type $2$, $op _ i$ is in the following format:

```
$2$ $a$ $b$
```

This corresponds to a Type $2$ operation with the given integers being $a$ and $b$.

If the $i$\-th operation is of Type $3$, $op _ i$ is in the following format:

```
$3$ $a$
```

This corresponds to a Type $3$ operation with the given integer being $a$.

## Output

Let the number of Type $3$ operations be $q$. Print $q$ lines. The $i$\-th line $(1 \leq i \leq q)$ should contain the nest number reported in the $i$\-th Type $3$ operation.

## Output

Let the number of Type $3$ operations be $q$. Print $q$ lines. The $i$\-th line $(1 \leq i \leq q)$ should contain the nest number reported in the $i$\-th Type $3$ operation.

## Sample Input 1

```
6 8
1 2 4
1 3 6
3 2
2 4 5
3 2
1 4 2
3 4
3 2
```

## Sample Output 1

```
4
5
2
5
```

In the operations given, the pigeons move as shown in the figure below:

![](https://gitee.com/chen-houchao/images/raw/master/img/20250301213559005.png)

The nest numbers to be reported for the Type $3$ operations are $4,5,2,5$. Print `4`, `5`, `2`, `5` on separate lines.

## Sample Input 2

```
1 2
1 1 1
3 1
```

## Sample Output 2

```
1
```

The destination nest of a Type $1$ operation may be the same as the nest the pigeon is currently in.

## Sample Input 3

```
30 15
3 3
2 8 30
2 12 15
2 2 17
1 19 1
2 7 30
3 12
3 8
2 25 26
1 13 10
1 16 10
2 16 29
2 1 21
2 6 11
1 21 8
```

## Sample Output 3

```
3
15
7
```

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;

void solve() {
  int N;
  cin >> N;
  // 实际巢穴就可以想象为一个酒店的实际房间，标签就相当于房间的门牌号
  vector<unordered_set<int>> physical_nests(N + 1);  // 每个实际巢穴中的鸽子
  unordered_map<int, int> label_to_physical;   // 标签到实际巢穴的映射
  unordered_map<int, int> physical_to_label;   // 实际巢穴到标签的映射
  unordered_map<int, int> pigeon_to_physical;  // 鸽子对应的实际巢穴
  for (int i = 1; i <= N; i++) {
    physical_nests[i].insert(i);
    label_to_physical[i]  = i;
    physical_to_label[i]  = i;
    pigeon_to_physical[i] = i;
  }
  // 准备工作完毕

  int Q;
  cin >> Q;
  while (Q--) {
    int opeType;
    cin >> opeType;
    if (opeType == 1) {  // 操作1,将鸽子a移动到b巢穴
      int a, b;
      cin >> a >> b;
      int nest = pigeon_to_physical[a];
      physical_nests[nest].erase(a);
      int target_nest       = label_to_physical[b];
      pigeon_to_physical[a] = target_nest;
      physical_nests[target_nest].insert(a);
    } else if (opeType == 2) {  // 操作2,交换巢穴1和巢穴2
      int a, b;
      cin >> a >> b;
      int phy_nest_a = label_to_physical[a];
      int phy_nest_b = label_to_physical[b];
      // 更换房间的门牌号，同时更换门牌号对应的实际房间
      physical_to_label[phy_nest_a] = b;
      physical_to_label[phy_nest_b] = a;
      label_to_physical[a]          = phy_nest_b;
      label_to_physical[b]          = phy_nest_a;
    } else if (opeType == 3) {  // 操作3,输出鸽子a所在的巢穴
      int a;
      cin >> a;
      int phy_nest = pigeon_to_physical[a];
      // 输出实际房间现在对应的门牌号
      cout << physical_to_label[phy_nest] << endl;
    }
  }
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);

  solve();
  return 0;
}
```

