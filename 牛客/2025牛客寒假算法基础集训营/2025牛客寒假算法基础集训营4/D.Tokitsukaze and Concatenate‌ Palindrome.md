# D.Tokitsukaze and Concatenate‌ Palindrome

![image-20250323124212728](https://gitee.com/chen-houchao/images/raw/master/202503231242893.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  int n, m;  // 字符串a和b的长度
  cin >> n >> m;
  string a, b;  // 字符串a和b
  cin >> a >> b;
  // 让a及其长度n始终大于另一边
  if (n < m) {
    swap(n, m);
    swap(a, b);
  }

  // 统计每种字母出现的次数
  int cnt_a[26] = { 0 }, cnt_b[26] = { 0 };
  for (auto &c : a) cnt_a[c - 'a']++;
  for (auto &c : b) cnt_b[c - 'a']++;

  // 消除两边都有的共同字符
  for (int i = 0; i < 26; i++) {
    int sub_num = min(cnt_a[i], cnt_b[i]);
    cnt_a[i] -= sub_num;
    cnt_b[i] -= sub_num;
  }

  // 消除更长的字符串（也就是现在的字符串a）能够跨过回文中心线的部分
  int len = (n + m) / 2 - m;
  for (int i = 0; i < 26; i++) {
    // len*2是为了防止越界，""是为了取偶数部分
    int sub_num = min(len * 2, (cnt_a[i] >> 1) << 1);
    cnt_a[i] -= sub_num;
    len -= sub_num / 2;
  }

  // 统计剩下需要替换的字母
  int ans = 0;
  for (int i = 0; i < 26; i++) {
    ans += cnt_a[i] + cnt_b[i];
  }
  // 最后有一半需要替换
  cout << ans / 2 << endl;
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

