# [B-小红的数组取数](https://ac.nowcoder.com/acm/contest/117763/B)

![image-20251002155518938](https://gitee.com/chen-houchao/images/raw/master/202510021555053.png)

## 代码

​	根据题意，就是要使得选取的ax尽可能小，选取的by尽可能大，直接使用min_element和max_element找到最大元素和最小元素的下标即可。

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int ll

void solve() {
  int n;
  cin >> n;
  vector<int> a(n), b(n);
  for (int i = 0; i < n; i++) cin >> a[i];
  for (int i = 0; i < n; i++) cin >> b[i];
  auto idxA = min_element(a.begin(), a.end()) - a.begin();
  auto idxB = max_element(b.begin(), b.end()) - b.begin();
  cout << idxA + 1 << " " << idxB + 1 << endl;
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

