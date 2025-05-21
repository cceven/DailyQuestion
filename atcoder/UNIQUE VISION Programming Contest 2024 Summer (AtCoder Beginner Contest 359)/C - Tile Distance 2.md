# C - Tile Distance 2 

------

Time Limit: 2 sec / Memory Limit: 1024 MB

Score : 350350 points

## Problem Statement

The coordinate plane is covered with $2\times1$ tiles. The tiles are laid out according to the following rules:

-   For an integer pair $(i,j)$, the square $A _ {i,j}=\lbrace(x,y)\mid i\leq x\leq i+1\wedge j\leq y\leq j+1\rbrace$ is contained in one tile.
-   When $i+j$ is even, $A _ {i,j}$ and $A _ {i + 1,j}$ are contained in the same tile.

Tiles include their boundaries, and no two different tiles share a positive area.

Near the origin, the tiles are laid out as follows:

![](https://gitee.com/chen-houchao/images/raw/master/202503132353625.png)

Takahashi starts at the point $(S _ x+0.5,S _ y+0.5)$ on the coordinate plane.

He can repeat the following move as many times as he likes:

-   Choose a direction (up, down, left, or right) and a positive integer $n$. Move $n$ units in that direction.

Each time he enters a tile, he pays a toll of $1$.

Find the minimum toll he must pay to reach the point $(T _ x+0.5,T _ y+0.5)$.

## Constraints

-   $0\leq S _ x\leq2\times10 ^ {16}$
-   $0\leq S _ y\leq2\times10 ^ {16}$
-   $0\leq T _ x\leq2\times10 ^ {16}$
-   $0\leq T _ y\leq2\times10 ^ {16}$
-   All input values are integers.

## Input

The input is given from Standard Input in the following format:

```
$S _ x$ $S _ y$
$T _ x$ $T _ y$
```

## Output

Print the minimum toll Takahashi must pay.

## Sample Input 1

```
5 0
2 5
```

## Sample Output 1

```
5
```

For example, Takahashi can pay a toll of $5$ by moving as follows:

![](https://gitee.com/chen-houchao/images/raw/master/202503132353435.png)

-   Move left by $1$. Pay a toll of $0$.
-   Move up by $1$. Pay a toll of $1$.
-   Move left by $1$. Pay a toll of $0$.
-   Move up by $3$. Pay a toll of $3$.
-   Move left by $1$. Pay a toll of $0$.
-   Move up by $1$. Pay a toll of $1$.

It is impossible to reduce the toll to $4$ or less, so print `5`.

## Sample Input 2

```
3 1
4 1
```

## Sample Output 2

```
0
```

There are cases where no toll needs to be paid.

## Sample Input 3

```
2552608206527595 5411232866732612
771856005518028 7206210729152763
```

## Sample Output 3

```
1794977862420151
```

Note that the value to be output may exceed the range of a $32$\-bit integer.

## 代码

![fc2c63dd7c8eb5745b12d68489802303_720](https://gitee.com/chen-houchao/images/raw/master/202503140008944.png)

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;

void solve() {
  ll s_x, s_y, t_x, t_y;
  cin >> s_x >> s_y >> t_x >> t_y;
  // 打表找出规律，先将两个点移到砖块左边
  if ((s_x + s_y) & 1) s_x--;
  if ((t_x + t_y) & 1) t_x--;

  ll diff_x = abs(t_x - s_x);
  ll diff_y = abs(t_y - s_y);
  // 输出这里，对于diff_x更大的情况这里是化简之后的结果
  cout << (diff_y + max(diff_x, diff_y)) / 2;
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);
  int t = 1;
  // cin >> t;
  while (t--) solve();
  return 0;
}
```

