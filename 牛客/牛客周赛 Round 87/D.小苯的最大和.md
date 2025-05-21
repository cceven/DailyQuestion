# [D.小苯的最大和](https://ac.nowcoder.com/acm/contest/105623/D)

![image-20250330230554211](https://gitee.com/chen-houchao/images/raw/master/202503302305303.png)

## 代码

**动态规划**

​	每次比较**删除当前数及当前数前一个（删除两个）**和**删除当前数及前两个(删除三个）**以及**不删除当前数的情况**

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int ll

void solve() {
  int n;
  cin >> n;
  vector<int> dp(n + 1, INT_MIN);  // 动态规划，存储第i个数的最大值
  vector<int> a(n + 1);            // 存储数
  dp[0] = 0;
  for (int i = 1; i <= n; i++) {
    cin >> a[i];
    dp[i] = dp[i - 1] + a[i];  // 不删除当前数的情况
    // 删除当前一个和前一个的情况
    if (i >= 2) {
      // 比较删除两个和不删除的情况
      dp[i] = max(dp[i], dp[i - 2]);
    }
    // 删除当前一个和前两个的情况
    if (i >= 3) {
      // 比较不删除当前数和删除三个的情况
      dp[i] = max(dp[i], dp[i - 3]);
    }
  }
  cout << dp[n] << endl;
}

signed main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);
  int t = 1;
  cin >> t;
  while (t--) solve();
  return 0;
}
```

