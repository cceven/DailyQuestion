#数学 #高精度 #模拟
[无穷无尽的小数](https://ac.nowcoder.com/acm/contest/123788/D)
小数a的循环节为n，小数b的循环节为m，要计算$a-b$我们首先就要将它们的循环节对齐，对齐后的循环节一定是n和m的**最小公倍数**。即$L = \text{lcm}(n, m)$。
**借位处理（难点）**：
循环小数 $0.\overline{X}$ 其实等于分数 $\frac{X}{10^L - 1}$。我们要算 $0.\overline{A} - 0.\overline{B} = \frac{A - B}{10^L - 1}$。如果 $A < B$，结果是负的。但在题目语境下（$a>b$），这意味着我们实际上利用了整数部分的“1”来填补这个负数。借了整数部分的 1，相当于分子加了 $(10^L - 1)$。所以分子变成了 $A - B + 10^L - 1$。 而我们在代码里做高精度减法时，因为借位机制，算出的是 $10^L + A - B$（那个 $10^L$ 是溢出的那个借位位权）。比较一下 $(10^L + A - B)$ 和我们想要的 $(10^L - 1 + A - B)$，会发现正好差 **1**。

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int ll

// 求最大公因数
int gcd(int a, int b) {
  while (b) {
    int r = a % b;
    a     = b;
    b     = r;
  }
  return a;
}

// 求最小公倍数
int lcm(int a, int b) {
  return a / gcd(a, b) * b;
}

void solve() {
  int n, m;
  cin >> n >> m;
  string sa, sb;
  cin >> sa >> sb;

  int l = lcm(n, m);
  string fa, fb;
  for (int i = 0; i < l; i++) fa += sa;
  for (int i = 0; i < l; i++) fb += sb;

  int burrow = 0;
  vector<int> ans(l);
  // 大整数减法
  for (int i = l - 1; i >= 0; --i) {
    int valA = fa[i] - '0', valB = fb[i] - '0';
    ans[i] = valA - valB - burrow;
    if (ans[i] < 0) {
      ans[i] += 10;
      burrow = 1;
    } else {
      burrow = 0;
    }
  }

  // 处理无限循环小数导致的“汇率”不同问题
  if (burrow == 1) {
    int sub_burrow = 1;
    for (int i = l - 1; i >= 0; --i) {
      ans[i] -= sub_burrow;
      if (ans[i] < 0) {
        ans[i] += 10;
        sub_burrow = 1;
      } else {
        sub_burrow = 0;
        break;
      }
    }
  }

  cout << l << endl;
  for (int i = 0; i < l; i++) {
    cout << ans[i];
  }
}

signed main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);
  int t = 1;
  // cin >> t;
  while (t--) solve();
  return 0;
}

```






