# B.小红的好点对

![image-20250916202829210](https://gitee.com/chen-houchao/images/raw/master/202509162028379.png)

## 代码

使用map存储前面的点，每增加一个新的点都遍历新的点的四个方向来增加`cnt`。

- 时间复杂度为O(n)（实际上为O(4n)，常数可忽略）
- 空间复杂度为O(n)

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int ll

void solve() {
  int cnt = 0;
  map<pair<int, int>, bool> mp;
  int n;  // 点的数量
  cin >> n;
  vector<pair<int, int>> direc = {
    { 0,  1  },
    { 1,  0  },
    { 0,  -1 },
    { -1, 0  }
  };  // 四个方向
  for (int i = 0; i < n; i++) {
    int x, y;
    cin >> x >> y;
    for (int j = 0; j < 4; j++) {
      pair<int, int> new_point =
              make_pair(x + direc[j].first, y + direc[j].second);
      if (mp[new_point]) {
        cnt++;
      }
    }
    mp[make_pair(x, y)] = true;
  }
  cout << cnt << endl;
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

