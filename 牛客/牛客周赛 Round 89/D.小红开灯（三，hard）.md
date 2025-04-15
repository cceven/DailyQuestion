# [D.小红开灯（三，hard）](https://ac.nowcoder.com/acm/contest/107000/D)

![image-20250416004954848](https://gitee.com/chen-houchao/images/raw/master/202504160049995.png)

## 代码

![image-20250416005425475](https://gitee.com/chen-houchao/images/raw/master/202504160054503.png)

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

#define int ll
const int MOD = 1e9 + 7;

// 快速幂
int fastPow(int a, int b) {
  int res = 1;
  while (b > 0) {
    if (b & 1) {
      res = res * a % MOD;
    }
    a = a * a % MOD;
    b >>= 1;
  }
  return res;
}

void solve() {
  int n, k;
  cin >> n >> k;
  if (n == k) {
    // n==k的时候只有全开和全关两种状态
    cout << "2" << endl;
  } else {
    // 推导出来的公式
    if (k & 1)
      cout << fastPow(2, n) << endl;
    else
      cout << fastPow(2, n - 1) << endl;
  }
}

signed main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);

  int t = 1;
  // cin >> t;
  while (t--) {
    solve();
  }
  return 0;
}
```

