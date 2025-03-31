# [A.2025](https://ac.nowcoder.com/acm/contest/105825/A)

![image-20250331103610735](https://gitee.com/chen-houchao/images/raw/master/img/20250331103610977.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  string s;  // 字符串s
  cin >> s;
  int sum      = 1;      // 初始sum
  bool is_have = false;  // 是否有解
  // 开始遍历字符串s
  for (auto &c : s) {
    if (c == '-') {
      sum--;
    } else if (c == '*') {
      sum *= 2;
    }
    // 如果存在sum>=2025
    if (sum >= 2025) {
      is_have = true;
      break;
    }
  }

  // 输出结果
  if (is_have) {
    cout << "YES" << endl;
  } else {
    cout << "NO" << endl;
  }
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);
  int t = 1;
  // cin>>t;
  while (t--) solve();
  return 0;
}
```

