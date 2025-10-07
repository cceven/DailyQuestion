# C-小红抽卡

![image-20251002155715868](https://gitee.com/chen-houchao/images/raw/master/202510021557994.png)

## 代码

​	直接逻辑顺序然后输出即可。

- k需要模一下x，因为每抽了x次相当于重置了一下。
- 只有前x个数字会变化，x之后的数字不变。
- 最后其实就是前x个数字从后到前的k个数字依次在前面，原来前面的(x-k)个数字顺序不变地排在抽取的数字的后面。

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int ll

void solve() {
  int n, k, x;
  cin >> n >> k >> x;
  k %= x;
  vector<int> a(n + 1);
  for (int i = 1; i <= n; i++) {
    cin >> a[i];
  }
  for (int i = x - k + 1; i <= x; i++) {
    cout << a[i] << " ";
  }
  for (int i = 1; i <= x - k; i++) {
    cout << a[i] << " ";
  }
  for (int i = x + 1; i <= n; i++) {
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

