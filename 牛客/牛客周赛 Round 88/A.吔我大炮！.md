# [A.吔我大炮！](https://ac.nowcoder.com/acm/contest/106318/A)

![image-20250411211731065](https://gitee.com/chen-houchao/images/raw/master/202504112117227.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  int a, b, c;
  cin >> a >> b >> c;
  int damage = a * b;  // 计算伤害
  if (damage <= c) {
    cout << "YES" << endl;
  } else {
    cout << "NO" << endl;
  }
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

