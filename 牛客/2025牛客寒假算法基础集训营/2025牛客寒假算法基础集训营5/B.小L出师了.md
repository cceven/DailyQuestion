# B.小L出师了

![image-20250324090509929](https://gitee.com/chen-houchao/images/raw/master/202503240905233.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  int n, k, t;
  cin >> n >> k >> t;
  int ans = 0;
  n -= t;  // 首先让小L讲完
  // 相当于t根小木棍分区域，炸鸡最多能有t+1个区域，也就是最大值
  ans = min(n / k, t + 1);
  cout << ans << endl;
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

