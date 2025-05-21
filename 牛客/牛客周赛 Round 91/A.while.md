# A.while

![image-20250506231718529](https://gitee.com/chen-houchao/images/raw/master/202505062317773.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int ll

void solve() {
  string s;
  cin >> s;
  string stan = "while";
  int cnt     = 0;
  for (int i = 0; i < s.size(); i++) {
    if (s[i] != stan[i]) cnt++;
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

