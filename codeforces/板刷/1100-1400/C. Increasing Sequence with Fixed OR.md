# C. Increasing Sequence with Fixed OR

time limit per test: 2 seconds

memory limit per test: 512 megabytes

input: standard input

output: standard output

You are given a positive integer $n$. Find the **longest** sequence of positive integers $a=[a_1,a_2,\ldots,a_k]$ that satisfies the following conditions, and print the sequence:

-   $a_i\le n$ for all $1\le i\le k$.
-   $a$ is strictly increasing. That is, $a_i&gt;a_{i-1}$ for all $2\le i\le k$.
-   $a_i\,|\,a_{i-1}=n$ for all $2\le i\le k$, where $|$ denotes the [bitwise OR operation](https://en.wikipedia.org/wiki/Bitwise_operation#OR).

## **Input**

Each test contains multiple test cases. The first line contains the number of test cases $t$ ($1 \le t \le 1000$). Description of the test cases follows.

The only line of each test case contains one integer $n$ ($1\le n\le 10^{18}$).

It's guaranteed that the sum of lengths of the longest valid sequences does not exceed $5\cdot 10^5$.

## **Output**

For each testcase, print two lines. In the first line, print the length of your constructed sequence, $k$. In the second line, print $k$ positive integers, denoting the sequence. If there are multiple longest sequences, you can print any of them.

## Example

### Input

```
4
1
3
14
23
```

### Output

```
1
1
3
1 2 3
4
4 10 12 14
5
7 18 21 22 23
```

## 代码

直接从`n`的第一位`1`开始遍历每一位，如果当前位在`n`中为`1`，并且当前不为`n`，那么直接把当前位翻转为`0`后的值插入到结果之中

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  ll n;
  cin >> n;
  vector<ll> ans;
  // 从最高位开始遍历
  for (int i = 63; i >= 0; i--) {
    ll cur_num = (1LL << i);  // 首先找到2^i
    // 如果当前的2^i在n之中，并且不等于n，那么直接插入到结果之中
    if ((cur_num & n) == cur_num && cur_num != n) {
      // 插入将n中的2^i
      ans.emplace_back(n - cur_num);
    }
  }
  // 最后插入n本身
  ans.push_back(n);
  // 输出答案
  cout << ans.size() << endl;
  for (int i = 0; i < ans.size(); i++) cout << ans[i] << " ";
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

### 判断当前位在`n`中是否存在

使用`(curr_num & n) == curr_num`判断当前位在`n`中是否存在

### 将某一位`1`进行翻转

使用`n - curr_num`（`curr_num = 2 ^ i `)