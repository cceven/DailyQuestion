# [F-小红的排列构造](https://ac.nowcoder.com/acm/contest/117763/F)

![image-20251002160901015](https://gitee.com/chen-houchao/images/raw/master/202510021609125.png)

## 代码

​	我们把2 1，这种称之为1个2-环。没有1-环的情况下（也就是所有位置都需要交换），需要操作的次数k=累加（环的数字数-1）=n-环的数量。

​	现在去看环的数量。环最多就是所有都是2-环的情况，为floor(n/2)。环最少的情况就是n-环。那么可以得到操作的次数的范围：ceil(n/2)-n-1。

​	判断操作次数合理之后，就可以开始构造环。通过操作次数k我们可以得到环的数量C。那我们就先构造C-1个2-环，然后剩下的数字全部一起构成一个环就可以了。

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int ll

void solve() {
  int n, k;
  cin >> n >> k;
  vector<int> a(n + 1);

  // 环的个数为1-floor(n/2)
  int kmin = ceil(n / 2.0), kmax = n - 1;
  if (k < kmin || k > kmax) {
    cout << -1 << endl;
    return;
  }

  int C = n - k;  // 需要的环的个数，公式来源：n-环个数=操作次数
  // 先构造C-1个2-环
  int used = 0;
  for (int i = 0; i < C - 1; i++) {
    int x = 2 * i + 1, y = 2 * i + 2;
    a[x] = y;
    a[y] = x;
    used += 2;
  }
  // 然后剩下的数构成一个环
  for (int i = used + 1; i <= n - 1; i++) {
    a[i] = i + 1;
  }
  a[n] = used + 1;

  // 输出
  for (int i = 1; i <= n; i++) {
    cout << a[i] << " ";
  }
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

