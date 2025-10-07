# D-小红的好数对

![image-20251002160037398](https://gitee.com/chen-houchao/images/raw/master/202510021600499.png)

## 代码

​	拼接数字A和数字B，那么得到的数字N=A*10\^m+B（m为B的位数），由于10=-1(mod11)，所以原式可以变为N=A\*(-1)\^m+B(mod11)。如果想要最后的结果是11的倍数，那么就有以下两种情况：

- m是偶数：A+B=0(mod11)
- m是奇数：A=B(mod11)

​	综上，我们可以创造cnt[11]记录所有数字模11后的取值，然后直接在cnt中找匹配的数字即可。

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int ll

// 计算数字的位数
static inline int digit_len(int x) {
  int c = 0;
  while (x) {
    c++;
    x /= 10;
  }
  return c ? c : 1;
}

void solve() {
  int n;
  cin >> n;
  vector<int> a(n);
  for (int i = 0; i < n; i++) cin >> a[i];

  int cnt[11] = { 0 };
  for (int i = 0; i < n; i++) {
    cnt[a[i] % 11]++;
  }

  int ans = 0;
  for (int i = 0; i < n; i++) {
    int m  = digit_len(a[i]);
    int rb = a[i] % 11;
    int rt;
    if (m & 1) {
      rt = rb;
    } else {
      rt = (11 - rb) % 11;
    }
    ans += cnt[rt];
    if (rt == rb) ans--;
  }
  cout << ans;
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

