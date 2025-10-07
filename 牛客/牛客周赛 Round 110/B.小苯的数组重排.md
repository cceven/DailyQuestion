# B.小苯的数组重排

![image-20250927193642998](https://gitee.com/chen-houchao/images/raw/master/202509271936096.png)

## 代码

这道题的本质就是要选出两个只加1次的数字，其他数字均加两次。所以排序后找到最小的两个数字就可以了。

```cpp
#include <bits/stdc++.h>
#define endl "\n"
#define int long long
using namespace std;
 
void solve() {
  int n;
  cin >> n;
  vector<int> a(n);
  for (int i = 0; i < n; i++) cin >> a[i];
  sort(a.begin(), a.end());
  int S = 0;
  S += a[0];
  S += a[1];
  for (int i = 2; i < n; i++) {
    S += a[i] * 2;
  }
  cout << S << endl;
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

