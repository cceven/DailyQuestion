# A.小L的三则运算

![image-20250324083528358](https://gitee.com/chen-houchao/images/raw/master/202503240835713.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;

void solve() {
  ll ans;
  char c;
  cin >> ans >> c;
  switch (c) {
    case '+':
      cout << ans - 1 << " " << "1";
      break;
    case '-':
      cout << ans + 1 << " " << "1";
      break;
    case '*':
      cout << ans << " " << "1";
      break;
  }
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);

  solve();
  return 0;
}
```

