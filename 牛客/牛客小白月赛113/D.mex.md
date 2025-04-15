# [D.mex](https://ac.nowcoder.com/acm/contest/105825/D)

![image-20250402150837826](https://gitee.com/chen-houchao/images/raw/master/202504021508263.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  int n;  // 数组中的元素数量
  cin >> n;
  vector<ll> a(n);                       // 数组
  bool is_same = true, is_zero = false;  // 是否所有元素相同，是否有元素0
  for (int i = 0; i < n; i++) {
    cin >> a[i];

    if (a[i] == 0) is_zero = true;
    if (i >= 1 && a[i] != a[i - 1]) is_same = false;
  }

  // 如果所有数字都相同，那么不用操作
  if (is_same) {
    cout << "0";
    return;
  }
  // 如果没有0，那么无解
  if (!is_zero) {
    cout << "-1";
    return;
  }

  // 首先排序
  sort(a.begin(), a.end());
  ll ans = 0;
  for (int i = 1; i < n; i++) {
    // 注意防止出现负数（当两个数字相同的时候会出现-1）
    ans += max(0LL, a[i] - a[i - 1] - 1);
  }
  // 最后还要操作一次把最后一组变为0
  cout << ans + 1;
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

