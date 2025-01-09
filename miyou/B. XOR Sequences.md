## XOR Sequences

https://codeforces.com/contest/1979/problem/B

### 题面翻译

给你两个不同的非负整数 $x$ 和 $y$。考虑两个无穷序列 $a _ 1, a _ 2, a _ 3, \ldots$ 和 $b _ 1, b _ 2, b _ 3, \ldots$，其中

- $a _ n = n \oplus x$；
- $b _ n = n \oplus y$。

例如，有了 $x = 6$ 之后，序列 $a$ 的前 $8$ 个元素将如下所示：$[7, 4, 5, 2, 3, 0, 1, 14, \ldots]$。

你的任务是找出序列 $a$ 和 $b$ 的最长公共子序列的长度。换句话说，找出最大整数 $m$ ，使得 $a _ i = b _ j, a _ {i + 1} = b _ {j + 1}, \ldots, a _ {i + m - 1} = b _ {j + m - 1}$ 对于某个 $i, j \ge 1$。

### 题目描述

You are given two distinct non-negative integers $ x $ and $ y $ . Consider two infinite sequences $ a_1, a_2, a_3, \ldots $ and $ b_1, b_2, b_3, \ldots $ , where

- $ a_n = n \oplus x $ ;
- $ b_n = n \oplus y $ .

Here, $ x \oplus y $ denotes the [bitwise XOR](https://en.wikipedia.org/wiki/Bitwise_operation#XOR) operation of integers $ x $ and $ y $ .

For example, with $ x = 6 $ , the first $ 8 $ elements of sequence $ a $ will look as follows: $ [7, 4, 5, 2, 3, 0, 1, 14, \ldots] $ . Note that the indices of elements start with $ 1 $ .

Your task is to find the length of the longest common subsegment $ ^\dagger $ of sequences $ a $ and $ b $ . In other words, find the maximum integer $ m $ such that $ a_i = b_j, a_{i + 1} = b_{j + 1}, \ldots, a_{i + m - 1} = b_{j + m - 1} $ for some $ i, j \ge 1 $ .

 $ ^\dagger $ A subsegment of sequence $ p $ is a sequence $ p_l,p_{l+1},\ldots,p_r $ , where $ 1 \le l \le r $ .

### 输入格式

Each test consists of multiple test cases. The first line contains a single integer $ t $ ( $ 1 \le t \le 10^4 $ ) — the number of test cases. The description of the test cases follows.

The only line of each test case contains two integers $ x $ and $ y $ ( $ 0 \le x, y \le 10^9, x \neq y $ ) — the parameters of the sequences.

### 输出格式

For each test case, output a single integer — the length of the longest common subsegment.

### 样例 #1

#### 样例输入 #1

```
4
0 1
12 4
57 37
316560849 14570961
```

##### 样例输出 #1

```
1
8
4
33554432
```

### 提示

In the first test case, the first $ 7 $ elements of sequences $ a $ and $ b $ are as follows:

 $ a = [1, 2, 3, 4, 5, 6, 7,\ldots] $

 $ b = [0, 3, 2, 5, 4, 7, 6,\ldots] $

It can be shown that there isn't a positive integer $ k $ such that the sequence $ [k, k + 1] $ occurs in $ b $ as a subsegment. So the answer is $ 1 $ .

In the third test case, the first $ 20 $ elements of sequences $ a $ and $ b $ are as follows:

 $ a = [56, 59, 58, 61, 60, 63, 62, 49, 48, 51, 50, 53, 52, 55, 54, \textbf{41, 40, 43, 42}, 45, \ldots] $

 $ b = [36, 39, 38, 33, 32, 35, 34, 45, 44, 47, 46, \textbf{41, 40, 43, 42}, 53, 52, 55, 54, 49, \ldots] $

It can be shown that one of the longest common subsegments is the subsegment $ [41, 40, 43, 42] $ with a length of $ 4 $ .

### 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;

int lowbit(const int &n)
{
    return n & (-n);
}
void solve()
{
    int x, y;
    cin >> x >> y;

    cout << lowbit(x ^ y) << endl; // 输出x和y异或的最低位
}

int main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int t; // t组数据
    cin >> t;
    while (t--)
    {
        solve();
    }
    return 0;
}
```

本题为一道结论题

通过观察输入输出样例，发现输出都是`2的n次幂`，并且是对应`x`和`y`异或后的`lowbit`的大小，故直接写。