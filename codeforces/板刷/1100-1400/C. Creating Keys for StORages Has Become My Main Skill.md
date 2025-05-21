# C. Creating Keys for StORages Has Become My Main Skill

time limit per test: 2 seconds

memory limit per test: 256 megabytes

input: standard input

output: standard output

Akito still has nowhere to live, and the price for a small room is everywhere. For this reason, Akito decided to get a job at a bank as a key creator for storages.

In this magical world, everything is different. For example, the key for a storage with the code $(n, x)$ is an array $a$ of length $n$ such that:

-   $a_1 \ | \ a_2 \ | \ a_3 \ | \ \ldots \ | \ a_n = x$, where $a \ | \ b$ is the [bitwise "OR"](https://en.wikipedia.org/wiki/Bitwise_operation#OR) of numbers $a$ and $b$.
-   $\text{MEX}(\{ a_1, a_2, a_3, \ldots, a_n \})$$^{\text{∗}}$ is maximized among all such arrays.

Akito diligently performed his job for several hours, but suddenly he got a headache. Substitute for him for an hour; for the given $n$ and $x$, create any key for the storage with the code $(n, x)$.

$^{\text{∗}}$$\text{MEX}(S)$ is the minimum non-negative integer $z$ such that $z$ is not contained in the set $S$ and all $0 \le y \lt z$ are contained in $S$.

## **Input**

The first line contains the number $t$ ($1 \le t \le 10^4$) — the number of test cases.

In the only line of each test case, two numbers $n$ and $x$ ($1 \le n \le 2 \cdot 10^5, 0 \le x \lt 2^{30}$) are given — the length of the array and the desired value of the bitwise "OR".

It is guaranteed that the sum of $n$ across all test cases does not exceed $2 \cdot 10^5$.

## **Output**

For each test case, output $n$ integers $a_i$ ($0 \le a_i \lt 2^{30}$) — the elements of the key array that satisfy all the conditions.

If there are multiple suitable arrays, output any of them.

## Example

### Input

```
9
1 69
7 7
5 7
7 3
8 7
3 52
9 11
6 15
2 3
```

### Output

```
69
6 0 3 4 1 2 5
4 1 3 0 2
0 1 2 3 2 1 0
7 0 6 1 5 2 4 3
0 52 0
0 1 8 3 0 9 11 2 10
4 0 3 8 1 2
0 3
```

## 代码

​	首先定义一个数组`ans`大小为`n`，并且所有都初始化赋值为`x`，保证条件一（也就是所有数的或一定为`x`）。

​	然后从开始遍历`0`到`n-2`判断是否符合要求，如果不符合要求那么直接中断。如果符合要求那么继续遍历。	同时设置一个`bool`类型的变量`is_break`判断是否提前中断了，如果没有提前中断，那么可以判断`n-1`是否符合要求并赋值给`ans`的最后一个数（最大化条件二，使得`ans`更加连续）。如果提前中断了且`n-1`不符合要求，那么最后一个数为`x`同样保证了条件一。

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  int n, x;  // 希望n个数的或为x
  cin >> n >> x;

  int cur_num = 0;  // 当前异或的结果
  // 结果，初始化为x，保证一定满足条件1（即所有数的或等于x）
  vector<int> ans(n, x);
  bool is_break = false;  // 没有被中断，每个都顺利赋值
  for (int i = 0; i < n - 1; i++) {
    // 判断进行当前的或操作后的所有的1是否都在x中存在
    if (((cur_num | i) & x) == (cur_num | i)) {
      ans[i] = i;
      cur_num |= i;
    } else {  // 如果不存在，说明条件2中断，已找到
      is_break = true;
      break;
    }
  }

  // 如果没有中断，那么可以尝试进一步更新条件二，看看n-1是否满足
  if (!is_break && (cur_num | (n - 1)) == x) {
    ans[n - 1] = n - 1;
  }

  // 输出答案
  for (int i = 0; i < ans.size(); i++) {
    cout << ans[i] << " ";
  }
  cout << endl;
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

