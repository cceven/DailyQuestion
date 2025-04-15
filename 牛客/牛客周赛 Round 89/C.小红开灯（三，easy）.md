# [C.小红开灯（三，easy）](https://ac.nowcoder.com/acm/contest/107000/C)

![image-20250414011242633](https://gitee.com/chen-houchao/images/raw/master/202504140112797.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

#define int ll
const int MOD = 1e9 + 7;

// 带有模的快速幂
int fastPow(int a, int b) {
  int result = 1;
  a %= MOD;
  while (b > 0) {
    if (b & 1) {
      result = (1LL * result * a) % MOD;
    }
    a = (1LL * a * a) % MOD;
    b /= 2;
  }
  return result;
}

void solve() {
  int n, k;
  cin >> n >> k;
  // 打表发现的结论
  cout << fastPow(2, n - k + 1) << endl;
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

复习了一下快速幂

![image-20250414011323386](https://gitee.com/chen-houchao/images/raw/master/202504140113441.png)
