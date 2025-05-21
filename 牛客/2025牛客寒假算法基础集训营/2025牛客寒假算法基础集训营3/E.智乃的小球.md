# E.[智乃的小球](https://ac.nowcoder.com/acm/contest/95335/E)

![image-20250313183047296](https://gitee.com/chen-houchao/images/raw/master/202503131830474.png)

## 代码

二分答案，幽灵碰撞（不考虑碰撞，互换速度，直接就是穿过去）

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;

ll countPairs(const ll &t, const vector<ll> &u, const vector<ll> &v) {
  ll res = 0;
  ll p1 = 0, p2 = 0;  // 两个指针，寻找范围
  for (auto &x : u) {
    while (p1 < v.size() && v[p1] < x) p1++;
    while (p2 < v.size() && v[p2] <= x + t) p2++;
    res += p2 - p1;
  }
  return res;
}

void solve() {
  ll n, k;  // 小球的数量，求第k次碰撞的时间
  cin >> n >> k;

  // 输入小球情况
  vector<ll> u, v;  // 分别存储速度为1和-1的小球
  for (ll i = 0; i < n; i++) {
    ll pos, speed;
    cin >> pos >> speed;
    if (speed == 1) {
      u.push_back(pos);
    } else {
      v.push_back(pos);
    }
  }
  sort(u.begin(), u.end());
  sort(v.begin(), v.end());

  // 开始二分答案
  ll l = 0, r = INT_MAX;
  double ans = (double)INT_MAX;
  while (l <= r) {
    ll mid    = l + (r - l) / 2;
    ll curr_k = countPairs(mid, u, v);
    if (curr_k >= k) {
      r = mid - 1;
    } else {
      ans = 1.0 * mid;
      l   = mid + 1;
    }
  }
  // 如果不能达到k次碰撞，那么直接输出结果
  if (ans == (double)INT_MAX) {
    cout << "No";
    return;
  }

  cout << "Yes" << endl;
  // 这里ans需要除2是因为我们进行测试只计算了单方进行行驶，但实际是双方进行行驶，也就是说速度两倍，时间减半
  cout << fixed << setprecision(6) << (ans + 1) / 2.0;
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

