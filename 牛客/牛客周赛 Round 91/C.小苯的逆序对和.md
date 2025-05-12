# C.小苯的逆序对和

![image-20250507003934067](https://gitee.com/chen-houchao/images/raw/master/202505070039171.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int ll

void solve() {
  int n;
  cin >> n;

  int mx = 0, ans = 0;
  // 固定j，找左边最大值
  for (int j = 1; j <= n; j++) {
    int x;
    cin >> x;
    if (x < mx) {
      ans = max(ans, mx + x);
    }

    mx = max(mx, x);
  }
  cout << ans << endl;
}

signed main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);
  int t = 1;
  cin >> t;
  while (t--) solve();
  return 0;
}
```

