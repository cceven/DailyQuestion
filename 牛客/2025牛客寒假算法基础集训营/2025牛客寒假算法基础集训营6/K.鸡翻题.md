# K.鸡翻题

![image-20250328142555366](https://gitee.com/chen-houchao/images/raw/master/img/20250328142555558.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  int x, y;
  cin >> x >> y;
  bool is_same = false;
  if (!(y & 1)) {
    // 如果是偶数，那么一定无解
    is_same = false;
  } else {
    // 如果是奇数，那么判断当前要求的左边一页(y/2)和当前的左边一页(x)的奇偶性是否相同
    is_same = (x & 1) == ((y / 2) & 1);
  }
  cout << (is_same ? "YES" : "NO") << endl;
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

