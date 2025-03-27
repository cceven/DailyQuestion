# I.小L的数学题

![image-20250324093038089](https://gitee.com/chen-houchao/images/raw/master/202503240930329.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  int n, m;  // n->m
  cin >> n >> m;
  if (n == 0 & m == 0)
    // 如果都是0，那么直接输出Yes
    cout << "Yes" << endl;
  else if (n == 0 || m == 0)
    // 如果其中一个是0，那么不能完成转换
    cout << "No" << endl;
  else
    // 如果n和m都不是0，那么可以完成转换
    cout << "Yes" << endl;
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

