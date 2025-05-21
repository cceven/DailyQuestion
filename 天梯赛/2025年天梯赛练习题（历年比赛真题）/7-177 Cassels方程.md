# **7-177 Cassels方程**

分数 10

作者 陈越

单位 浙江大学

Cassels方程是一个在数论界产生了巨大影响的不定方程：*x*2+*y*2+*z*2=3*x**yz*。该方程有无穷多自然数解。

本题并不是要你求解这个方程，只是判断给定的一组 (*x*,*y*,*z*) 是不是这个方程的解。

## 输入格式：

输入在第一行给出一个不超过 10 的正整数 *N*，随后 *N* 行，每行给出 3 个正整数 0<*x*≤*y*≤*z*≤1000。

## 输出格式：

对于每一组输入，如果是一组解，就在一行中输出 `Yes`，否则输出 `No`。

## 输入样例：

```in
2
1 1 1
5 6 7
```

## 输出样例：

```out
Yes
No
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
  int x, y, z;
  cin >> x >> y >> z;
  if (pow(x, 2) + pow(y, 2) + pow(z, 2) == 3 * x * y * z)
    cout << "Yes\n";
  else
    cout << "No\n";
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);
  int N;
  cin >> N;
  while (N--) solve();
  return 0;
}
```

