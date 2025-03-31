## C.Tokitsukaze and Balance String (hard)

![image-20250323001845320](https://gitee.com/chen-houchao/images/raw/master/202503230018411.png)

## 代码

![image-20250323001818780](https://gitee.com/chen-houchao/images/raw/master/202503230018823.png)

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

const int MOD = 1e9 + 7;

// 快速幂
ll fastPow(ll a, ll b) {
  a      = a % MOD;
  ll ans = 1;
  while (b != 0) {
    if (b & 1) {
      ans = (ans * a) % MOD;
    }
    a = (a * a) % MOD;
    b = (b >> 1);
  }
  return ans;
}

void solve() {
  int n;
  cin >> n;
  string s;
  cin >> s;

  // 如果只有一个，那么直接输出结果
  if (n == 1) {
    if (s[0] == '?') {
      cout << "2" << endl;
    } else {
      cout << "1" << endl;
    }
    return;
  }

  // 寻找中间的'?'数量
  int cnt = 0;
  for (int i = 1; i < n - 1; i++) {
    if (s[i] == '?') cnt++;
  }

  // 下面为推导出来的结论
  ll num1 = fastPow(2, cnt) * (n - 2), num2 = fastPow(2, cnt) * 2;
  int f1, f2;
  if (s[0] == '?' && s.back() == '?') {
    f1 = 2;
    f2 = 2;
  } else if (s[0] == '?' || s.back() == '?') {
    f1 = 1;
    f2 = 1;
  } else if (s[0] == s.back()) {
    f1 = 1;
    f2 = 0;
  } else if (s[0] != s.back()) {
    f1 = 0;
    f2 = 1;
  }

  ll ans = f1 * num1 + f2 * num2;
  cout << ans % MOD << endl;
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

