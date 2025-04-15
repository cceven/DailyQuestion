# [**F - ABCBA**](https://atcoder.jp/contests/abc398/tasks/abc398_f)

![image-20250402130226096](https://gitee.com/chen-houchao/images/raw/master/202504021302286.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

// 马拉车算法
vector<int> palindrome(const string &s) {
  string t = "$#";
  for (auto &c : s) {
    t += c;
    t += "#";
  }
  int n = t.size();

  vector<int> p(n, 0);
  int center = 1, r = 1;
  for (int i = 1; i < n; i++) {
    int mirror_c = 2 * center - i;

    p[i] = min(p[mirror_c], r - i);

    while (i + p[i] + 1 < n && i - p[i] - 1 >= 0 &&
           t[i + p[i] + 1] == t[i - p[i] - 1]) {
      p[i]++;
    }

    if (i + p[i] > r) {
      center = i;
      r      = i + p[i];
    }
  }

  return p;
}

void solve() {
  string s;  // 待填充字符串
  cin >> s;
  int n = s.size();

  vector<int> r = palindrome(s);  // // r[i] 表示以 i 为中心的回文串的半径
  int k = 0;                      // 需要补充的字符串的长度
  for (int i = 1; i < r.size(); i++) {
    // 如果当前的回文串到达了最后一个字符
    if (r[i] + i == r.size() - 1) {
      k = s.size() - r[i];
      break;
    }
  }

  cout << s;  // 首先输入前面的
  // 输入后面填充的字符
  for (int i = 0; i < k; i++) {
    cout << s[k - 1 - i];
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

