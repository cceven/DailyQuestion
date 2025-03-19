# E.Tokitsukaze and Dragon's Breath

![image-20250318130922971](https://gitee.com/chen-houchao/images/raw/master/202503181309101.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;

void solve() {
  int n, m;
  cin >> n >> m;
  vector<vector<ll>> a(n + 1, vector<ll>(m + 1, 0));
  for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= m; j++) cin >> a[i][j];
  }

  unordered_map<ll, ll> mp1, mp2;
  for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= m; j++) {
      mp1[i + j] += a[i][j];  // 存储左下到右上的斜线
      mp2[i - j] += a[i][j];  // 存储从左上到右下的斜线
    }
  }

  ll ans = 0;
  // 遍历每一个点，求得以每一个点为中心进行攻击时的最大值
  for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= m; j++) {
      ans = max(ans, (ll)mp1[i + j] + mp2[i - j] - a[i][j]);
    }
  }
  cout << ans << endl;
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

一个矩阵，从一个点出发往四个顶点进行延伸。我们可以得到，从左上到右下的每一个点的`x - y`的值是相等的，从左下到右上的每一个点的`x + y`是相等的。所以可以将左下到右上和从左上到右下的点分别进行存储。

![image-20250318131048218](https://gitee.com/chen-houchao/images/raw/master/202503181310276.png)