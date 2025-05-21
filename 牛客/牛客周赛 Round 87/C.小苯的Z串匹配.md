# [C.小苯的Z串匹配](https://ac.nowcoder.com/acm/contest/105623/C)

![image-20250330223426365](https://gitee.com/chen-houchao/images/raw/master/202503302234455.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int long long

void solve() {
  int n;  // 数组a的初始长度
  cin >> n;
  vector<int> a(n);
  for (auto &x : a) cin >> x;
  string S;  // 字符串S
  cin >> S;

  int cnt = 0;  // 需要修改的次数
  for (int i = 0; i < n; i++) {
    if (S[i] == '<' && !(a[i] < 0)) {
      a[i] = -1;
      cnt++;
    } else if (S[i] == '>' && !(a[i] > 0)) {
      a[i] = 1;
      cnt++;
    } else if (S[i] == 'Z' && !(a[i] * a[i - 1] > 0)) {
      a[i] = a[i - 1];
      cnt++;
    }
  }
  cout << cnt << endl;
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

