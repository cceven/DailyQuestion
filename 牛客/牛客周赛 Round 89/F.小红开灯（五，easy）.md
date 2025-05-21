# [F.小红开灯（五，easy）](https://ac.nowcoder.com/acm/contest/107000/F)

![image-20250416175657361](https://gitee.com/chen-houchao/images/raw/master/202504161756575.png)

## 代码

树形dp

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int ll

int dp[100001][3];      // 三种状态
vector<int> g[100001];  // 相邻边

void dfs(int x, int px) {
  dp[x][0]++;
  int min_value = INT_MAX, min_idx;
  for (auto y : g[x]) {
    if (y == px) continue;  // 如果是父亲直接跳过
    dfs(y, x);
    dp[x][0] +=
            min(dp[y][1], dp[y][2]);  // 操作当前节点，孩子只要不被操作就可以
    dp[x][1] += min(dp[y][1], dp[y][2]);  // 之后要进一步操作
    dp[x][2] += dp[y][1];  // 当前节点不被操作，孩子也不被操作

    // 找到最小的dp[y][1]
    if (min_value > dp[y][0] - min(dp[y][1], dp[y][2])) {
      min_value = dp[y][0] - min(dp[y][1], dp[y][2]);
    }
  }

  // 如果不是叶子节点
  if (g[x].size() > 1 || x == 1) {
    // 选取孩子中最小的dp[y][1]
    dp[x][1] += min_value;
  } else {
    dp[x][1] = INT_MAX;
  }
}

void solve() {
  int n;
  cin >> n;
  // 插入边
  for (int i = 1; i <= n - 1; i++) {
    int u, v;
    cin >> u >> v;
    g[u].push_back(v);
    g[v].push_back(u);
  }
  // 从根节点开始dfs
  dfs(1, 0);
  // 找到最小的答案
  int ans = min(dp[1][1], dp[1][2]);
  cout << ans << endl;
}

signed main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);

  int t = 1;
  // cin >> t;
  while (t--) {
    solve();
  }
  return 0;
}
```

