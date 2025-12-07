[无穷无尽的力量](https://ac.nowcoder.com/acm/contest/123788/A)
![[Pasted image 20251203124203.png]]
## 代码
直接使用string的初始化方式来拼接字符串。
```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int ll

void solve() {
  int n;
  cin >> n;
  cout << string(n, 'a') + "b" + string(n, 'a') << endl;
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