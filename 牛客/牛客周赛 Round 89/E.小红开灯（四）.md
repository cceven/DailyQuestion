# [E.小红开灯（四）](https://ac.nowcoder.com/acm/contest/107000/E)

![image-20250415213106098](https://gitee.com/chen-houchao/images/raw/master/202504152131211.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

#define int ll

int cnt = 0;
vector<pair<int, int>> ans;

// 对两个点进行处理
void pro(pair<int, int> a, pair<int, int> b) {
  if (a.first > a.first) swap(a, b);
  for (int i = a.first; i < b.first; i++) {
    ans.push_back({ a.first, a.second });
    a.first++;
    ans.push_back({ a.first, a.second });
    cnt++;
  }
  if (a.second == b.second) {
    return;
  }

  if (a.second > b.second) swap(a, b);
  for (int i = a.second; i < b.second; i++) {
    ans.push_back({ a.first, a.second });
    a.second++;
    ans.push_back({ a.first, a.second });
    cnt++;
  }
}

void solve() {
  int n, m;
  cin >> n >> m;
  map<pair<int, int>, bool> mp;  // 存储所有关闭的灯的位置
  for (int i = 1; i <= n; i++) {
    string s;
    cin >> s;
    for (int j = 0; j < s.size(); j++) {
      if (s[j] == '0') {
        mp[{ i, j + 1 }] = true;
      }
    }
  }

  vector<pair<int, int>> stop_light;  // 需要处理的灯
  for (auto it = mp.begin(); it != mp.end(); it++) {
    pair<int, int> cur_pos = it->first;
    if (it->second == true) {
      stop_light.emplace_back(cur_pos);
    }
  }

  // 如果不需要处理
  if (stop_light.empty()) {
    cout << "0" << endl;
    return;
  }

  // 如果有奇数个待处理的灯
  if (stop_light.size() & 1) {
    cout << "-1" << endl;
    return;
  }

  // 开始进行处理
  for (int i = 0; i < stop_light.size(); i += 2) {
    pair<int, int> pre_pos = stop_light[i], cur_pos = stop_light[i + 1];
    pro(pre_pos, cur_pos);
  }

  // 输出结果
  cout << cnt << endl;
  for (int i = 0; i < ans.size(); i += 2) {
    cout << ans[i].first << " " << ans[i].second << " " << ans[i + 1].first
         << " " << ans[i + 1].second << endl;
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

