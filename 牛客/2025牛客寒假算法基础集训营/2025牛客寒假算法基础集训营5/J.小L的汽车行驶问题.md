# J.小L的汽车行驶问题

![image-20250324084719498](https://gitee.com/chen-houchao/images/raw/master/202503240847899.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  int n;
  cin >> n;
  string ope;  // 进行的操作
  cin >> ope;
  int cur_v = 0;  // 当前的速度
  ll ans    = 0;  // 行驶的总距离
  // 开始遍历操作
  for (auto &c : ope) {
    // 油门，速度直接加10
    if (c == '0') {
      cur_v += 10;
      ans += cur_v;
    } else if (c == '1') {
      // 刹车，速度减5，防止变为0
      cur_v = max(cur_v - 5, 0);
      ans += cur_v;
    } else if (c == '2') {
      int ori_v = cur_v;
      // 离合，速度减10，防止变为0
      cur_v = max(cur_v - 10, 0);
      ans += cur_v;
      // 1秒后恢复原来的速度
      cur_v = ori_v;
    }
  }

  cout << ans;
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

