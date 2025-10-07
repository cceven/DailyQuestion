# C.小苯的麦克斯

![image-20250927193827449](https://gitee.com/chen-houchao/images/raw/master/202509271938542.png)

## 代码

​	最优区间一定是某两个元素。证明：1.假设最优区间的最大值两边有一个不是0,那么直接搭配不是0的元素（MEX=0）2.如果两边都是0,那么继续延伸只可能导致结果更小。
​	所以遍历所有的两个元素，并更新ans就可以了

```cpp
#include <bits/stdc++.h>
#define endl "\n"
#define int  long long
using namespace std;
 
inline int mex2(int x, int y) {
  bool has0 = (x == 0 || y == 0);
  bool has1 = (x == 1 || y == 1);
  if (!has0) return 0;
  if (!has1) return 1;
  return 2;
}
 
void solve() {
  int n;
  cin >> n;
  vector<int> a(n);
  for (int i = 0; i < n; i++) cin >> a[i];
  int ans = LLONG_MIN;
  for (int i = 0; i < n - 1; i++) {
    int mx  = max(a[i], a[i + 1]);
    int MEX = mex2(a[i], a[i + 1]);
    ans     = max(ans, mx - MEX);
  }
  cout << ans << endl;
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

