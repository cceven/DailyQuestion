# A.小苯的数字染色

![image-20250927193502147](https://gitee.com/chen-houchao/images/raw/master/202509271935302.png)

## 代码

正整数中，除了数字1之外，其他的所有数字都能够通过多个2+多个3组成。

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
 
void solve() {
  int n;
  cin >> n;
  if (n == 1) {
    cout << "NO" << endl;
  } else {
    cout << "YES" << endl;
  }
  return;
}
 
int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);
  int t = 1;
  // cin>>t;
  while (t--) solve();
  return 0;
}
```

