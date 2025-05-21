# I.Tokitsukaze and Pajama Party

![image-20250318010014625](https://gitee.com/chen-houchao/images/raw/master/202503180100749.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;

void solve() {
  int n;
  cin >> n;
  string s;
  cin >> s;
  vector<int> cnt(n, 0);  // 存储到每个位置为止，拥有的字符u的个数
  int curr_sum = 0;
  for (int i = 0; i < n; i++) {
    if (s[i] == 'u') {
      curr_sum++;
    }
    cnt[i] = curr_sum;
  }

  int ans  = 0;
  auto pos = s.find("uwawauwa");
  while (pos != string::npos) {
    if (pos >= 2) ans += cnt[pos - 2];

    pos = s.find("uwawauwa", pos + 1);
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

