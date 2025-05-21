# [B.好字符串](https://ac.nowcoder.com/acm/contest/105825/B)

![image-20250331104310146](https://gitee.com/chen-houchao/images/raw/master/img/20250331104310369.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  int n;     // 字符串的长度
  string s;  // 字符串
  cin >> n >> s;
  int same_num = 0;  // 相邻数相同的个数
  for (int i = 1; i < n; i++) {
    // 如果和前面的字符相同，那么相同数增加
    if (s[i] == s[i - 1]) same_num++;
    // 如果相邻数相同的个数大于等于2,那么不符合结果，直接break
    if (same_num >= 2) {
      break;
    }
  }

  // 判定结果
  if (same_num <= 1) {
    cout << "YES" << endl;
  } else {
    cout << "NO" << endl;
  }
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

