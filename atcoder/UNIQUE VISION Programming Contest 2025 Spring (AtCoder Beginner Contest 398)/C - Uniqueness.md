# [**C - Uniqueness**](https://atcoder.jp/contests/abc398/tasks/abc398_c)

![image-20250402000307973](https://gitee.com/chen-houchao/images/raw/master/202504020003091.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int ll

void solve() {
  int N;  // 数组长度
  cin >> N;
  vector<int> A(N);
  unordered_map<int, int> cnt;  // 出现的次数，找到只出现一次的
  int ans = -1;
  for (int i = 0; i < N; i++) {
    cin >> A[i];
    cnt[A[i]]++;
  }

  int max_value = INT_MIN;  // 记录符合要求的最大数
  for (int i = 0; i < N; i++) {
    // 如果只出现了一次并且值更大，那么更新当前的答案
    if (cnt[A[i]] == 1 && A[i] > max_value) {
      max_value = A[i];
      ans       = i + 1;
    }
  }
  cout << ans;
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

