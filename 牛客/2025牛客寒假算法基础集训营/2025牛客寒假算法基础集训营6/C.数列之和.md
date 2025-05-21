# C.数列之和

![image-20250328212151797](https://gitee.com/chen-houchao/images/raw/master/img/20250328212151873.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  ll k;
  cin >> k;
  k *= 2;  // 本来应该的位置（所有偶数的情况）
  for (ll i = 4; i <= k; i *= 2) {
    // 计算缺少的2^p，每少一个就增加2
    k += 2;
  }
  cout << k << endl;
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

