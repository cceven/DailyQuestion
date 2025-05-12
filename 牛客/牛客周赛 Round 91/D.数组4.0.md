# D.数组4.0

![image-20250507101900449](https://gitee.com/chen-houchao/images/raw/master/202505071019653.png)

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

  unordered_map<int, int> cnt;  // 存储数字出现的个数
  for (int i = 0; i < n; i++) {
    int x;
    cin >> x;
    cnt[x]++;
  }

  int ans = 0;
  for (auto &[x, y] : cnt) {
    // 如果当前数前面的数不存在，说明是一个新的区间
    if (cnt.find(x - 1) == cnt.end()) {
      ans += 1;
      // 如果当前区间的大小为1
      if (cnt.find(x + 1) == cnt.end()) {
        ans += y - 1;
      }
    }
  }
  // 答案为ans-1
  cout << ans - 1 << endl;
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

