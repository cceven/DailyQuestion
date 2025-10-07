# [A-小红的阶梯](https://ac.nowcoder.com/acm/contest/117763/A)

![image-20251002155339859](https://gitee.com/chen-houchao/images/raw/master/202510021553049.png)

## 代码

​	直接条件判断。

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int ll

void solve() {
  int a1, a2, a3;
  cin >> a1 >> a2 >> a3;
  if (a1 + 1 == a2 && a2 + 1 == a3)
    cout << "Yes" << endl;
  else
    cout << "No" << endl;
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

