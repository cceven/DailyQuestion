# [G.升！龙！](https://ac.nowcoder.com/acm/contest/106318/G)

![image-20250415183750231](https://gitee.com/chen-houchao/images/raw/master/202504151837369.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;
using ll = long long;
#define int ll

void solve() {
  int n, q;  // n个节点，q次查询
  cin >> n >> q;

  vector<int> a(n + 1, 0);  // 存储每个节点的权值
  for (int i = 1; i <= n; i++) cin >> a[i];

  vector<int> fa(n + 1, 0);      // 存储每个节点的父亲
  vector<vector<int>> g(n + 1);  // 存储每个节点的孩子
  for (int i = 2; i <= n; i++) {
    cin >> fa[i];
    g[fa[i]].emplace_back(i);
  }

  // 存储每个节点对应的最左的孩子和最右的孩子
  vector<int> L(n + 1, -1), R(n + 1, -1);
  vector<int> son_mx(n + 1);  // 存储每个节点对应的最大的子权值
  vector<int> pre(n + 1);     // 存储每个节点的权前缀和
  vector<int> leafs(1);       // 存储叶子结点
  vector<int> mp(n + 1);      // 存储叶子节点的编号
  auto dfs = [&](auto &&self, int u) -> int {
    pre[u] = pre[fa[u]] + a[u];  // 更新前缀
    L[u] = R[u] = u;
    // 如果是叶子节点
    if (g[u].empty()) {
      mp[u] = leafs.size();
      leafs.emplace_back(u);
      //			son_mx[u] = a[u];
      return son_mx[u] = a[u];
    }

    // 非叶子结点
    for (auto v : g[u]) {
      son_mx[u] = max(son_mx[u], self(self, v));
    }
    // 更新左叶子和右叶子
    L[u] = L[g[u][0]];
    R[u] = R[g[u].back()];

    // 更新当前节点的最大子权值
    son_mx[u] += a[u];
    return son_mx[u];
  };

  dfs(dfs, 1);

  vector<int> pre_mx(leafs.size()), suf_mx(leafs.size() + 1);
  // 更新每个叶子结点的前缀最大值
  for (int i = 1; i < leafs.size(); i++) {
    pre_mx[i] = max(pre_mx[i - 1], pre[leafs[i]]);
  }

  // 更新每个叶子结点的后缀最大值
  for (int i = leafs.size() - 1; i >= 1; i--) {
    suf_mx[i] = max(suf_mx[i + 1], pre[leafs[i]]);
  }

  while (q--) {
    int x, y;
    cin >> x >> y;
    int l = mp[L[x]], r = mp[R[x]];
    int ans = max(pre_mx[l - 1], suf_mx[r + 1]);
    ans     = max(ans, pre[fa[x]]);
    ans     = max(ans, pre[y] + son_mx[x]);
    cout << ans << endl;
  }
}

signed main() {
  int t = 1;
  //	cin>>t;
  while (t--) {
    solve();
  }
  return 0;
}
```

