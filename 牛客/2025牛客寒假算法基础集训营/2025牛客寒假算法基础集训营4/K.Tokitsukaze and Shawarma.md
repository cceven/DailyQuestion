# K.Tokitsukaze and Shawarma

![image-20250318010247958](https://gitee.com/chen-houchao/images/raw/master/202503180102028.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;

void solve() {
  int x, y, z, a, b, c;
  cin >> x >> y >> z >> a >> b >> c;
  cout << max({ x * a, y * b, z * c }) << endl;
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

