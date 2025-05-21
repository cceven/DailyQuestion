# [G.小红开灯（五，hard）](https://ac.nowcoder.com/acm/contest/107000/G)

![image-20250416182027459](https://gitee.com/chen-houchao/images/raw/master/202504161820598.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int ll

int dp[100001][3];      // 三种状态
vector<int> g[100001];  // 相邻边
vector<pair<int, int>> ans;
int p[100001];  // 存储操作的子节点

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
      min_idx   = y;
    }
  }

  // 如果不是叶子节点
  if (g[x].size() > 1 || x == 1) {
    // 选取孩子中最小的dp[y][1]
    dp[x][1] += min_value;
    p[x] = min_idx;
  } else {
    dp[x][1] = INT_MAX;
  }
}

void dfs2(int x, int px, int ope_type) {
  if (ope_type == 1) ans.push_back({ x, p[x] });
  // 还可以使用另外一种
  // if(ope_type == 0) ans.push_back({x, px});

  for (auto y : g[x]) {
    if (y == px) continue;

    if (ope_type == 0) {
      if (dp[y][1] < dp[y][2])
        dfs2(y, x, 1);
      else
        dfs2(y, x, 2);
    } else if (ope_type == 1) {
      if (y == p[x])
        dfs2(y, x, 0);
      else {
        if (dp[y][1] < dp[y][2])
          dfs2(y, x, 1);
        else
          dfs2(y, x, 2);
      }
    } else {
      dfs2(y, x, 1);
    }
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
  int res = min(dp[1][1], dp[1][2]);
  if (res == dp[1][1])
    dfs2(1, 0, 1);
  else
    dfs2(1, 0, 2);

  // 输出答案
  cout << ans.size() << endl;
  for (auto it : ans) cout << it.first << " " << it.second << endl;
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

