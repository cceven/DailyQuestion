# B. Variety is Discouraged

time limit per test: 1.5 seconds

memory limit per test: 256 megabytes

input: standard input

output: standard output

Define the score of an arbitrary array $b$ to be the length of $b$ minus the number of distinct elements in $b$. For example:

-   The score of $[1, 2, 2, 4]$ is $1$, as it has length $4$ and only $3$ distinct elements ($1$, $2$, $4$).
-   The score of $[1, 1, 1]$ is $2$, as it has length $3$ and only $1$ distinct element ($1$).
-   The empty array has a score of $0$.

You have an array $a$. You need to remove some **non-empty** contiguous subarray from $a$ **at most** once.

More formally, you can do the following **at most** once:

-   pick two integers $l$, $r$ where $1 \le l \le r \le n$, and
-   delete the contiguous subarray $[a_l,\ldots,a_r]$ from $a$ (that is, replace $a$ with $[a_1,\ldots,a_{l - 1},a_{r + 1},\ldots,a_n]$).

Output an operation such that the score of $a$ is **maximum**; if there are multiple answers, output one that **minimises** the final length of $a$ after the operation. If there are still multiple answers, you may output any of them.

## **Input**

The first line contains an integer $t$ ($1 \le t \le 10^4$) — the number of testcases.

The first line of each testcase contains an integer $n$ ($1 \le n \le 2 \cdot 10^5$) — the length of the array $a$.

The second line of each testcase contains $n$ integers $a_1,a_2,\ldots,a_n$ ($1 \le a_i \le n$).

The sum of $n$ across all testcases does not exceed $2 \cdot 10^5$.

## **Output**

For each testcase, if you wish to not make a move, output $0$.

Otherwise, output two integers $l$ and $r$ ($1 \le l \le r \le n$), representing the left and right bound of the removed subarray.

The removed subarray should be chosen such that the score is maximized, and over all such answers choose any of them that minimises the final length of the array.

## Example

### Input

```
3
1
1
5
1 1 1 1 1
4
2 1 3 2
```

### Output

```
1 1
0
2 3
```

**Note**

In the first testcase, we have two options:

-   do nothing: the score of $[1]$ is $1-1=0$.
-   remove the subarray with $l=1$, $r=1$: we remove the only element, and we get an empty array with score $0$.

Therefore, the maximum score possible is $0$. However, since we need to additionally minimise the final length of the array, we **must** output the second option with $l=r=1$. Note that the first option of doing nothing is **incorrect**, since it has a longer final length.

In the second testcase, no subarray is selected, so after which $a$ is still $[1, 1, 1, 1, 1]$. This has length $5$ and $1$ distinct element, so it has a score of $5 - 1 = 4$. This can be proven to be a shortest array which maximises the score.

In the third testcase, the subarray selected is $[2, \color{red}1, \color{red}3, 2]$, after which $a$ becomes $[2, 2]$. This has length $2$ and $1$ distinct element, so it has a score of $2 - 1 = 1$. This can be proven to be a shortest array which maximises the score.

## 代码

​	需要的结果是`数组的长度 - 不同数字的个数`，那么就可以知道，如果个数大于`1`的数字一定是贡献了加分的，只要删去了一个频率大于`1`的数字，那么得分就会减少，肯定小于原始数组的得分。考虑频率为`1`的数字，删去后对得分没有影响，所以就可以知道，我们修改数组后的得分一定是小于等于原始数组的得分的，所以其实也就是求频率为1的子数组的最大长度来减小数组长度。

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  int n;  // 数组的原始长度
  cin >> n;
  vector<int> a(n);
  unordered_map<int, int> cnt;  // 统计每个数出现的次数
  for (auto &x : a) {
    cin >> x;
    cnt[x]++;  // 统计每个数出现的次数
  }

  int l = -1, r = -1;  // 结果窗口
  int temp_l = 0;      // 当前窗口的左边界
  for (int temp_r = 0; temp_r < n; temp_r++) {
    int cur_num = a[temp_r];

    if (cnt[cur_num] == 1) {
      // 如果当前数的频率是1，那么尝试更新最终结果
      if (temp_r - temp_l >= r - l) {
        // 如果当前窗口的长度大于等于结果窗口那么更新结果窗口
        l = temp_l;
        r = temp_r;
      }
    } else {
      // 如果当前数不符合条件，那么更新窗口左边界
      temp_l = temp_r + 1;
    }
  }
  // 如果没有符合条件的子数组，那么直接输出0
  if (l == -1 && r == -1) {
    cout << "0" << endl;
  } else {
    // 输出索引+1
    cout << l + 1 << " " << r + 1 << endl;
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

