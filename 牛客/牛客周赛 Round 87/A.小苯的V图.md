# [A.小苯的V图](https://ac.nowcoder.com/acm/contest/105623/A)

![image-20250330222959094](https://gitee.com/chen-houchao/images/raw/master/202503302229227.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  int a, b, c;  // 输入三个数
  cin >> a >> b >> c;
  // 判断是否符合条件
  if (a > b && b < c) {
    cout << "YES";
  } else {
    cout << "NO";
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

