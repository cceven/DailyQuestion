# [B.小苯的数字切割](https://ac.nowcoder.com/acm/contest/105623/B)

![image-20250330223137975](https://gitee.com/chen-houchao/images/raw/master/202503302231057.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  string n;  // 整数n
  cin >> n;
  int ans = 0;  // 最终结果
  for (int i = 1; i < n.size(); i++) {
    int a = stoi(n.substr(0, i));  // a是前半部分的数字
    int b = stoi(n.substr(i));     // b是后半部分的数字
    // ans取a+b的最大值
    ans = max(ans, a + b);
  }
  cout << ans << endl;
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

