# [E.小苯的矩阵反转](https://ac.nowcoder.com/acm/contest/108038/E)

![image-20250507115559485](https://gitee.com/chen-houchao/images/raw/master/202505071155664.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int ll

const int dx[4] = { -1, 0, 1, 0 }, dy[4] = { 0, 1, 0, -1 };

void solve() {
  int n, m;
  cin >> n >> m;
  vector<string> a(n);
  vector<int> row(n, 0), col(m, 0);  // 每行或每列1的个数
  int cnt_sum = 0;                   // 1的总数

  for (int i = 0; i < n; i++) {
    cin >> a[i];
    for (int j = 0; j < m; j++) {
      if (a[i][j] == '1') {
        row[i]++;
        col[j]++;
        cnt_sum++;
      }
    }
  }

  // 多少行全1
  int cnt_row = 0;
  for (int i = 0; i < n; i++) {
    cnt_row += (row[i] == m);
  }

  // 多少列全1
  int cnt_col = 0;
  for (int j = 0; j < m; j++) {
    cnt_col += (col[j] == n);
  }
  // 1.原始矩阵符合条件。2.两行或两列全1
  if (cnt_sum == 0 || (cnt_row == 2 && cnt_sum == 2 * m) ||
      (cnt_col == 2 && cnt_sum == 2 * n)) {
    cout << "YES" << endl;
    return;
  }

  // 3.十字形
  bool ok = false;
  for (int i = 0; i < n; i++) {
    for (int j = 0; j < m; j++) {
      if (a[i][j] == '1') continue;

      bool no = false;
      for (int k = 0; k < 4; k++) {
        int x = i + dx[k], y = j + dy[k];
        // 如果越界了
        if (x < 0 || x >= n || y < 0 || y >= m) continue;

        // 如果旁边有0，不符合条件
        if (a[x][y] == '0') {
          no = true;
          break;
        }
      }

      if (!no) {
        // 十字形除了中心全1
        if (cnt_sum == n + m - 2) {
          ok = true;
          break;
        }
      }
    }
    // 如果找到了
    if (ok) {
      break;
    }
  }

  if (ok) {
    cout << "YES" << endl;
  } else {
    cout << "NO" << endl;
  }
}

signed main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);
  int t = 1;
  cin >> t;
  while (t--) solve();
  return 0;
}
```

