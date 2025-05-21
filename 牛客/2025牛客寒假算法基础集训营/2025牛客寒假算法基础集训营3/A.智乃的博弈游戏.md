# A.智乃的博弈游戏

![image-20250311173346751](https://gitee.com/chen-houchao/images/raw/master/202503111733867.png)

## 代码

​	结论：如果`n`是奇数，那么先手方必赢；如果`n`是偶数，那么先手方必输。

​	首先需要知道如果某一方拿到了`2`个石子的状态，那么必输。如果`n`是奇数，那么先手方可以通过每次只拿`1`个石头，让后手方始终处于偶数的状态，那么最终一定是后手方拿到`2`的状态，后手方输。如果`n`是偶数，需要知道与偶数互质的只能是奇数而不能是偶数，所以如果某一方拿到了偶数那么只能减去一个奇数让对手方仍然处于奇数状态，奇数方可以减去`1`让另一方又回到偶数状态，所以如果`n`是偶数的话那么先手方必败。

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;

void solve() {
  ll n;  // n个石头
  cin >> n;
  if (n & 1) {  // 如果n是奇数，那么先手方必赢
    cout << "Yes";
  } else {  // 如果n是偶数，那么先手方必输
    cout << "No";
  }
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);
  int t = 1;
  // cin >> t;
  while (t--) solve();
  return 0;
}
```

