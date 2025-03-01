# **B - Make Target**

------

Time Limit: 2 sec / Memory Limit: 1024 MB

Score : 200200 points

## Problem Statement

> **Overview**: Create an $N \times N$ pattern as follows.```
> ###########
> #.........#
> #.#######.#
> #.#.....#.#
> #.#.###.#.#
> #.#.#.#.#.#
> #.#.###.#.#
> #.#.....#.#
> #.#######.#
> #.........#
> ###########
> ```

You are given a positive integer $N$.

Consider an $N \times N$ grid. Let $(i,j)$ denote the cell at the $i$\-th row from the top and the $j$\-th column from the left. Initially, no cell is colored.

Then, for $i = 1,2,\dots,N$ in order, perform the following operation:

-   Let $j = N + 1 - i$.
-   If $i \leq j$, fill the rectangular region whose top-left cell is $(i,i)$ and bottom-right cell is $(j,j)$ with black if $i$ is odd, or white if $i$ is even. If some cells are already colored, overwrite their colors.
-   If $i &gt; j$, do nothing.

After all these operations, it can be proved that there are no uncolored cells. Determine the final color of each cell.

## Constraints

-   $1 \leq N \leq 50$
-   All input values are integers.

## Input

The input is given from Standard Input in the following format:

```
$N$
```

## Output

Print $N$ lines. The $i$\-th line should contain a length-$N$ string $S_i$ representing the colors of the $i$\-th row of the grid after all operations, as follows:

-   If cell $(i,j)$ is finally colored black, the $j$\-th character of $S_i$ should be `#`.
-   If cell $(i,j)$ is finally colored white, the $j$\-th character of $S_i$ should be `.`.

## Sample Input 1

```
11
```

## Sample Output 1

```
###########
#.........#
#.#######.#
#.#.....#.#
#.#.###.#.#
#.#.#.#.#.#
#.#.###.#.#
#.#.....#.#
#.#######.#
#.........#
###########
```

This matches the pattern shown in the **Overview**.

## Sample Input 2

```
5
```

## Sample Output 2

```
#####
#...#
#.#.#
#...#
#####
```

Colors are applied as follows, where `?` denotes a cell not yet colored:

```
         i=1      i=2      i=3      i=4      i=5
?????    #####    #####    #####    #####    #####
?????    #####    #...#    #...#    #...#    #...#
????? -> ##### -> #...# -> #.#.# -> #.#.# -> #.#.#
?????    #####    #...#    #...#    #...#    #...#
?????    #####    #####    #####    #####    #####
```

## Sample Input 3

```
8
```

## Sample Output 3

```
########
#......#
#.####.#
#.#..#.#
#.#..#.#
#.####.#
#......#
########
```

## Sample Input 4

```
2
```

## Sample Output 4

```
##
##
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
  vector<vector<char>> martix(N + 1, vector<char>(N + 1));
  for (int i = 1; i <= N; i++) {
    int j = N + 1 - i;

    // 开始判断
    if (i <= j) {
      for (int m = i; m <= j; m++) {
        for (int n = i; n <= j; n++) {
          martix[m][n] = (i & 1 ? '#' : '.');
        }
      }
    }
  }

  for (int i = 1; i <= N; i++) {
    for (int j = 1; j <= N; j++) {
      cout << martix[i][j];
    }
    cout << endl;
  }
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);

  solve();
  return 0;
}
```

