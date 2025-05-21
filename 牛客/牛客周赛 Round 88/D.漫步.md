# [D.漫步](https://ac.nowcoder.com/acm/contest/106318/D)

![image-20250411222446491](https://gitee.com/chen-houchao/images/raw/master/202504112224572.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  int x;
  cin >> x;
  for (int i = 0; i <= 30; i++) {
    int cur_num = (1LL << i);  // 2^i
    // 如果当前数字在x中为0并且当前位小于x的最高位1
    if ((cur_num & x) != cur_num && cur_num < x) {
      cout << cur_num << endl;
      return;
    }
  }
  cout << "-1" << endl;
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

