# [F.小苯的ovo2.0](https://ac.nowcoder.com/acm/contest/105623/F)

![image-20250331002830992](https://gitee.com/chen-houchao/images/raw/master/202503310028076.png)

## 代码

[题解](https://www.bilibili.com/video/BV1rvZNYqETt?spm_id_from=333.788.videopod.episodes&vd_source=d00bc79c7901f27a447b550b4ddaec3c&p=6)

![image-20250331002809672](https://gitee.com/chen-houchao/images/raw/master/202503310028728.png)

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  string S;  // 字符串S
  cin >> S;
  int n = S.size();  // 字符的数量

  // 统计把[l,r]区间内的换为'v'，其余换为'o'的"ovo"数量
  auto cal = [&](const int &l, const int &r) {
    string s = S;
    // 首先把[l, r]之内的更换为'v'，之外的更换为'o'
    for (int i = 0; i < n; i++) {
      if (s[i] != '?') continue;  // 如果不是'?'那么直接跳过

      if (i < l || i > r) {
        // 区间之外的换为'o'
        s[i] = 'o';
      } else {
        //[l,r]之内的换为'v'
        s[i] = 'v';
      }
    }

    // 开始统计数量
    int o = 0, ov = 0, ovo = 0;
    for (int i = 0; i < n; i++) {
      if (s[i] == 'o') {
        o++;
        ovo += ov;
      } else {
        ov += o;
      }
    }
    return ovo;
  };

  int ans = 0;
  for (int l = 0; l < n; l++) {
    // 这里r从l-1开始遍历是为了有一次全为'o'的情况
    for (int r = l - 1; r < n; r++) {
      int cur_res = cal(l, r);
      ans         = max(ans, cur_res);
    }
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

