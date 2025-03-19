# **算法2-1 在顺序表 list 中查找元素 x**

分数 10

作者 陈越

单位 浙江大学

请编写程序，将 *n* 个整数存入顺序表，对任一给定整数 *x*，查找其在顺序表中的位置。

## 输入格式：

输入首先在第一行给出正整数 *n*（≤104）；随后一行给出 *n* 个 int 范围内的不重复的整数，数字间以空格分隔；最后一行给出待查找的元素 *x*，也是 int 范围内的整数。

## 输出格式：

在一行中输出 *x* 在顺序表中的位置，即数组下标。如果没找到，则输出 -1。注意数组下标从 0 开始。

## 输入样例 1：

```in
5
1 2 3 4 5
4
```

## 输出样例 1：

```out
3
```

## 输入样例 2：

```in
5
4 3 6 8 0
1
```

## 输出样例 2：

```out
-1
```

代码长度限制

16 KB

时间限制

400 ms

内存限制

64 MB

栈限制

8192 KB

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;

void solve() {
  int n;
  cin >> n;
  vector<int> nums(n);
  for (auto &n : nums) cin >> n;

  int x;
  cin >> x;
  auto pos = find(nums.begin(), nums.end(), x) - nums.begin();
  cout << (pos != nums.size() ? pos : -1);
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

