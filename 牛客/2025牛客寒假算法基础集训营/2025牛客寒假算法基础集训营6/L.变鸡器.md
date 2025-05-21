# L.变鸡器

![image-20250328150409443](https://gitee.com/chen-houchao/images/raw/master/img/20250328150409644.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  int n;  // 字符串的长度
  cin >> n;
  string s;  // 字符串
  cin >> s;
  bool is_able  = false;  // 是否含有'CHICKEN'
  string target = "CHICKEN";
  string remain_s;
  int i = 0, j = 0;
  while (i < n && j < 7) {
    if (s[i] == target[j]) {
      // 如果匹配
      if (++j == 7) is_able = true;
      i++;
    } else {
      // 如果不匹配
      remain_s += s[i];
      i++;
    }
  }
  // 如果无解
  if (!is_able) {
    cout << "NO" << endl;
    return;
  }
  // 加上剩余的s
  while (i < n) {
    remain_s += s[i];
    i++;
  }
  // 如果剩余的字符为奇数个，那么不能达到要求
  if (remain_s.size() & 1) {
    cout << "NO" << endl;
    return;
  }
  // 开始判断能否消除
  // 首先统计剩余字符中每一个字符的频率
  vector<int> cnt(26, 0);
  int max_cnt = 0;
  for (auto &c : remain_s) {
    cnt[c - 'A']++;
    max_cnt = max(max_cnt, cnt[c - 'A']);
  }
  // 如果存在某一个字符的频率超过了剩余字符的一半，那么不能消除
  if (max_cnt > remain_s.size() / 2) {
    cout << "NO" << endl;
  } else {
    cout << "YES" << endl;
  }
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

