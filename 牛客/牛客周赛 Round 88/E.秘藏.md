# [E.秘藏](https://ac.nowcoder.com/acm/contest/106318/E)

![image-20250411225850957](https://gitee.com/chen-houchao/images/raw/master/202504112258056.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int ll

void solve() {
  int n, k;
  cin >> n >> k;
  vector<int> a(n), b(n);
  for (auto &x : a) cin >> x;
  for (auto &x : b) cin >> x;

  // 分别为到达外世界i的最大金币，到达里世界i点的最大金币数
  vector<int> dp1(n, 0), dp2(n, 0);
  dp1[0] = a[0];       // 可以到达a[0]
  dp2[0] = LLONG_MIN;  // 不可达b[0]，所以初始化为负无穷
  for (int i = 1; i < n; i++) {
    // 到达a[i]的最大金币数量
    if (dp2[i - 1] >= k) {
      dp1[i] = max(dp1[i - 1], dp2[i - 1] - k) + a[i];
    } else {
      dp1[i] = dp1[i - 1] + a[i];
    }
    // 到达b[i]的最大金币数量
    if (dp1[i - 1] >= k) {
      dp2[i] = max(dp2[i - 1], dp1[i - 1] - k) + b[i];
    } else {
      dp2[i] = dp2[i - 1] + b[i];
    }
  }
  cout << max(dp1[n - 1], dp2[n - 1]);
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

