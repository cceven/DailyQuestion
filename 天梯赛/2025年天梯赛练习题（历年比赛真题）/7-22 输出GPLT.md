# **7-22 输出GPLT**

分数 20

作者 陈越

单位 浙江大学

给定一个长度不超过10000的、仅由英文字母构成的字符串。请将字符重新调整顺序，按`GPLTGPLT....`这样的顺序输出，并忽略其它字符。当然，四种字符（不区分大小写）的个数不一定是一样多的，若某种字符已经输出完，则余下的字符仍按`GPLT`的顺序打印，直到所有字符都被输出。

## 输入格式：

输入在一行中给出一个长度不超过10000的、仅由英文字母构成的非空字符串。

## 输出格式：

在一行中按题目要求输出排序后的字符串。题目保证输出非空。

## 输入样例：

```in
pcTclnGloRgLrtLhgljkLhGFauPewSKgt
```

## 输出样例：

```out
GPLTGPLTGLTGLGLL
```

代码长度限制

16 KB

时间限制

200 ms

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
  string in_info;
  cin >> in_info;
  for (auto &i : in_info) {
    i = toupper(i);
  }

  stack<char> alphas[4];
  for (auto &i : in_info) {
    if (i == 'G')
      alphas[0].push(i);
    else if (i == 'P')
      alphas[1].push(i);
    else if (i == 'L')
      alphas[2].push(i);
    else if (i == 'T')
      alphas[3].push(i);
  }

  while (!alphas[0].empty() || !alphas[1].empty() || !alphas[2].empty() ||
         !alphas[3].empty()) {
    if (!alphas[0].empty()) {
      cout << "G";
      alphas[0].pop();
    }
    if (!alphas[1].empty()) {
      cout << "P";
      alphas[1].pop();
    }
    if (!alphas[2].empty()) {
      cout << "L";
      alphas[2].pop();
    }
    if (!alphas[3].empty()) {
      cout << "T";
      alphas[3].pop();
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

- 可以创建`stack`数组
- `toupper()`只能对单个字符使用而不能直接对整个字符串使用