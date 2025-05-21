# C.智乃的Notepad(Easy version)

![image-20250312170153711](https://gitee.com/chen-houchao/images/raw/master/202503121701862.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;

// 返回共同前缀长度
int lcp(const string &a, const string &b) {
  int idx = 0;
  while (idx < a.size() && idx < b.size() && a[idx] == b[idx]) idx++;
  return idx;
}

void solve() {
  int n, m;
  cin >> n >> m;
  vector<string> s(n);
  int max_len = 0;
  for (auto &str : s) {
    cin >> str;
    max_len = max(max_len, (int)str.size());
  }
  int l, r;
  cin >> l >> r;

  sort(s.begin(), s.end());
  int sum = 0;
  for (int i = 0; i < n; i++) {
    sum += s[i].size() * 2;
    if (i) {
      sum -= lcp(s[i], s[i - 1]) * 2;
    }
  }
  cout << sum - max_len;
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

