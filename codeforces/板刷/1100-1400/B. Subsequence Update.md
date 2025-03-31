# B. Subsequence Update

time limit per test: 1.5 seconds

memory limit per test: 256 megabytes

input: standard input

output: standard output

After Little John borrowed expansion screws from auntie a few hundred times, eventually she decided to come and take back the unused ones.

But as they are a crucial part of home design, Little John decides to hide some in the most unreachable places — under the eco-friendly wood veneers.

You are given an integer sequence $a_1, a_2, \ldots, a_n$, and a segment $[l,r]$ ($1 \le l \le r \le n$).

You must perform the following operation on the sequence **exactly once**.

-   Choose any **subsequence**$^{\text{∗}}$ of the sequence $a$, and reverse it. Note that the subsequence does not have to be contiguous.

Formally, choose any number of indices $i_1,i_2,\ldots,i_k$ such that $1 \le i_1 \lt i_2 \lt \ldots \lt i_k \le n$. Then, change the $i_x$\-th element to the original value of the $i_{k-x+1}$\-th element simultaneously for all $1 \le x \le k$.

Find the **minimum value** of $a_l+a_{l+1}+\ldots+a_{r-1}+a_r$ after performing the operation.

$^{\text{∗}}$A sequence $b$ is a subsequence of a sequence $a$ if $b$ can be obtained from $a$ by the deletion of several (possibly, zero or all) element from arbitrary positions.

## **Input**

Each test contains multiple test cases. The first line contains the number of test cases $t$ ($1 \le t \le 10^4$). The description of the test cases follows.

The first line of each test case contains three integers $n$, $l$, $r$ ($1 \le l \le r \le n \le 10^5$) — the length of $a$, and the segment $[l,r]$.

The second line of each test case contains $n$ integers $a_1,a_2,\ldots,a_n$ ($1 \le a_{i} \le 10^9$).

It is guaranteed that the sum of $n$ over all test cases does not exceed $10^5$.

## **Output**

For each test case, output the minimum value of $a_l+a_{l+1}+\ldots+a_{r-1}+a_r$ on a separate line.

## Example

### Input

```
6
2 1 1
2 1
3 2 3
1 2 3
3 1 3
3 1 2
4 2 3
1 2 2 2
5 2 5
3 3 2 3 5
6 1 3
3 6 6 4 3 2
```

### Output

```
1
3
6
3
11
8
```

### **Note**

On the second test case, the array is $a=[1,2,3]$ and the segment is $[2,3]$.

After choosing the subsequence $a_1,a_3$ and reversing it, the sequence becomes $[3,2,1]$. Then, the sum $a_2+a_3$ becomes $3$. It can be shown that the minimum possible value of the sum is $3$.

## 代码

​	这个题目要求求指定索引`l`和`r`之间的数的和，需要指定几个数字进行一次颠倒。可以发现，如果同时选择了`r`右边的和`l`左边的数的话，就会导致无用的交换，最左边和最右边的数字还是不在`l`和`r`的区间之内。所以可以想到，只能选择`[0, r]`之间最小的`r - l + 1`个数或者`[l , n]`之间的`r - l + 1`个最小的数，两者取更小值。

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  int n, l, r;
  cin >> n >> l >> r;
  // 恢复为0开始的下标
  l--;
  r--;
  // 输入数组
  vector<int> a(n);
  for (auto &x : a) cin >> x;

  // 提取左数组
  vector<ll> l_vec(a.begin(), a.begin() + r + 1);
  sort(l_vec.begin(), l_vec.end());
  ll l_val = reduce(l_vec.begin(), l_vec.begin() + (r - l + 1), 0LL);
  // 提取右数组
  vector<ll> r_vec(a.begin() + l, a.end());
  sort(r_vec.begin(), r_vec.end());
  ll r_val = reduce(r_vec.begin(), r_vec.begin() + (r - l + 1), 0LL);
  // 以更小的数作为结果
  ll ans = min(l_val, r_val);
  cout << ans << endl;
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

### `reduce()函数`和`accumulate`函数需要注意

当涉及到`long long`类型的时候，`0`记得加上`LL`，不然最后返回的值还是`int`类型，导致结果错误。

![image-20250330122902250](https://gitee.com/chen-houchao/images/raw/master/202503301229299.png)