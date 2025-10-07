# E-小芳的排列构造

![image-20251002160537613](https://gitee.com/chen-houchao/images/raw/master/202510021605719.png)

## 代码

​	n作为最大值，不论是L或者是R中肯定都包含一次n。n-1作为第二大值，有一侧会被n阻挡，所以要么出现在L中要么出现在R中，肯定会出现一次。所以我们就得到了可以达到的最小值3n-1。最大值就是其他数字也各出现一次，即n*(n+3)/2。

​	那么我们就可以先从n-2遍历到1，找到需要出现一次的数字，然后依次从大大小构造链表就可以了。

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int ll

void solve() {
  int n, k;
  cin >> n >> k;

  if (n == 1) {
    if (k == 2)
      cout << "1" << endl;
    else
      cout << "-1\n";
    return;
  }

  int kmin = 3 * n - 1, kmax = n * (n + 3) / 2;
  if (k < kmin || k > kmax) {
    cout << "-1\n";
    return;
  }

  int t = k - kmin;  // 剩余需要满足的部分
  vector<int> take(n + 1);
  for (int i = n - 2; i >= 1; i--) {
    if (t >= i) {
      take[i] = 1;
      t -= i;
    }
  }

  list<int> lst;  // 最终的数列
  lst.push_back(n);
  lst.push_back(n - 1);
  for (int i = n - 2; i >= 1; i--) {
    if (take[i])
      lst.push_front(i);
    else {
      // 不需要的数字插入到第二个位置，这样既不计入L也不计入R
      auto it = lst.begin();
      lst.insert(++it, i);
    }
  }

  bool first = true;
  for (auto x : lst) {
    if (first) {
      cout << x;
      first = false;
    } else {
      cout << " " << x;
    }
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

