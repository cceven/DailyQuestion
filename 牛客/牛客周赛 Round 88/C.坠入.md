# [C.坠入](https://ac.nowcoder.com/acm/contest/106318/B)

![image-20250411220533256](https://gitee.com/chen-houchao/images/raw/master/202504112205372.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  vector<pair<double, double>> edges(3);
  for (int i = 0; i < 3; i++) {
    cin >> edges[i].first >> edges[i].second;
  }

  vector<pair<double, double>> mid(3);
  mid[0].first  = (edges[1].first + edges[2].first) / 2.0;
  mid[0].second = (edges[1].second + edges[2].second) / 2.0;
  mid[1].first  = (edges[0].first + edges[2].first) / 2.0;
  mid[1].second = (edges[0].second + edges[2].second) / 2.0;
  mid[2].first  = (edges[0].first + edges[1].first) / 2.0;
  mid[2].second = (edges[0].second + edges[1].second) / 2.0;
  for (int i = 0; i < 3; i++) {
    bool if_x = (mid[i].first == edges[i].first);
    bool if_y = (mid[i].second == edges[i].second);
    if (if_x || if_y) {
      cout << "YES" << endl;
      return;
    }
  }
  cout << "NO" << endl;
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

