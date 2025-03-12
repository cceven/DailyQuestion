# F.智乃的捉迷藏

![image-20250311184841424](https://gitee.com/chen-houchao/images/raw/master/202503111848489.png)

## 代码

![25840fab294a11e913663929c4b57fc](https://gitee.com/chen-houchao/images/raw/master/202503111849766.jpeg)

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;

void solve() {
  int n, a, b, c;
  cin >> n >> a >> b >> c;
  // 利用数学公式
  if (n <= a + b + c && a + b + c <= 2 * n) {
    cout << "Yes" << endl;
  } else {
    cout << "No" << endl;
  }
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

