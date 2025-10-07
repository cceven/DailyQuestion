# A.小红的直角三角形

![image-20250916201334212](https://gitee.com/chen-houchao/images/raw/master/202509162013482.png)

## 代码

题目已经说明了是不同的两个点并且不是原点，那么我们想要构成三角形就只需要保证两个点一个在X轴一个在Y轴上就行了。判断的方法就是x1和x2之间必须有且只能有1个为0，y1和y2之间必须有且只能有1个0。

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int ll

void solve() {
  int x1, y1, x2, y2;
  cin >> x1 >> y1 >> x2 >> y2;
  int x = (x1 == 0) + (x2 == 0);
  int y = (y1 == 0) + (y2 == 0);
  if (x == 1 && y == 1) {
    cout << "Yes" << endl;
    return;
  }

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

