[米斯蒂娅不想被吃掉](https://ac.nowcoder.com/acm/contest/124143/B)
![[Pasted image 20251214130848.png]]
```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int ll

void solve() {
  int n, x;
  cin >> n >> x;
  vector<int> a(n);
  for (int i = 0; i < n; i++) cin >> a[i];
  int pre_a = 0;  // 存储前一天剩余的处理量
  for (int i = 0; i < n; i++) {
    int tar_a =
            max(0LL, x - pre_a);  // 优先使用前一天的剩余量，再看还需要处理多少
    if (tar_a > a[i]) {           // 当天处理不了
      cout << "No" << endl;
      return;
    } else {  // 把今天剩下的留到明天用
      pre_a = a[i] - tar_a;
    }
  }
  cout << "Yes" << endl;
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