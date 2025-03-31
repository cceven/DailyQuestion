# 茕茕孑立之影

**构造**、**数论**

## ![image-20250121192732940](https://gitee.com/chen-houchao/images/raw/master/202501211927059.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;

void solve() {
  int n;
  cin >> n;
  // 一定符合要求的最小的质数（数据范围在10^9以内，所以取10^9+7）
  int ans = 1e9 + 7;
  vector<int> nums(n);
  for (int i = 0; i < n; i++) {
    cin >> nums[i];
    if (nums[i] == 1) {  // 如果有1那么肯定没有符合要求的数据，直接输出-1
      ans = -1;
    }
  }
  cout << ans << endl;
  return;
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);
  int T;
  cin >> T;
  while (T--) {
    solve();
  }
  return 0;
}
```

