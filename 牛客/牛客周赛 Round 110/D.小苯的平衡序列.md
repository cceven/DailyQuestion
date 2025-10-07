# D.小苯的平衡序列

![image-20250927194036351](https://gitee.com/chen-houchao/images/raw/master/202509271940462.png)

## 代码

​	首先需要知道一个性质。这里以1为base，假设去掉某个元素之后的中位数的位置在k这个位置，那么去掉这个元素之前的数组中位数的中位数一定在k或者k+1这两个位置。

- 在k+1的情况：去掉的元素在小于等于k的位置。
- 在k的情况：去掉的元素在大于k的位置。

​	所以这道题就直接对两种情况分别计算然后取最大值就可以了。

```cpp
#include <bits/stdc++.h>
#define endl "\n"
#define int  long long
using namespace std;
 
// 计算当前的平衡度
static inline int sumAbsToPivotAtIndex(
        const vector<int> &a, const vector<int> &pre, int m
) {
  int n     = a.size();
  int left  = m * a[m] - pre[m];                           // 左侧的平衡度
  int right = (pre[n] - pre[m + 1]) - (n - m - 1) * a[m];  // 右侧的平衡度
  return left + right;
}
 
void solve() {
  int n;
  cin >> n;
  vector<int> a(n);
  for (int i = 0; i < n; i++) cin >> a[i];
  sort(a.begin(), a.end());
  vector<int> pre(n + 1, 0);  // 前缀和
  for (int i = 0; i < n; i++) pre[i + 1] = pre[i] + a[i];
 
  int k = n / 2;
  // 两种情况的中位数
  int idxA = k - 1, idxB = k;
 
  int S1   = sumAbsToPivotAtIndex(a, pre, idxA);
  int S2   = sumAbsToPivotAtIndex(a, pre, idxB);
  int ans1 = S1 - (a.back() - a[idxA]);
  int ans2 = S2 - (a[idxB] - a[0]);
  int ans  = min(ans1, ans2);
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

