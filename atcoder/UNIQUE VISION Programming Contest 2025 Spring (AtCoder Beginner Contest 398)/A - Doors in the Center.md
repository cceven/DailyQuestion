# [**A - Doors in the Center**](https://atcoder.jp/contests/abc398/tasks/abc398_a)

![image-20250401235205473](https://gitee.com/chen-houchao/images/raw/master/202504012352570.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  int N;  // 字符串的长度
  cin >> N;
  string ans;
  // 计算'-'的数量和'='的数量，'='的数量只会是1或者是2，取决于N的奇偶性
  int equal_num = (N & 1) ? 1 : 2, minus_num = (N - equal_num) / 2;
  // 直接拼接字符串
  ans += string(minus_num, '-') + string(equal_num, '=') +
         string(minus_num, '-');
  cout << ans << endl;
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