# M.智乃的牛题

![image-20250311181029961](https://gitee.com/chen-houchao/images/raw/master/202503111810059.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;

void solve() {
  string standard_s = "nowcoder";
  sort(standard_s.begin(), standard_s.end());

  string s;
  cin >> s;
  sort(s.begin(), s.end());
  if (s == standard_s)
    cout << "happy new year";
  else
    cout << "I AK IOI";
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

