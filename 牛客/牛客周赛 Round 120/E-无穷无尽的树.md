[无穷无尽的树](https://ac.nowcoder.com/acm/contest/123788/E)
题目要求去找删除某个节点的子树中包含的所有叶子结点后，这个节点的子树中深度最深的节点有多少个。既然已经删除了所有的叶子结点，即深度最大的节点，那么剩下的深度最深的节点肯定就是之前删除的叶子节点的父亲了，也就是之前深度为maxDepth-1的节点。所以选定某个节点，我们只需要去找这个节点的子树中深度为maxDepth-1的节点有多少个就行了。

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int ll

const int MAXN = 2e5 + 5;
vector<int> adj[MAXN];    // 邻接矩阵
int depth[MAXN];          // 存储每个节点的深度
int max_depth[MAXN];      // 存储每个节点的最大深度
int timer = 0;            // 计时器，用于找子节点
int in[MAXN], out[MAXN];  // 存储每个节点的进入时间和离开时间
bool is_leaf[MAXN];       // 是否为叶子结点
vector<int> non_leaf_at_depth[MAXN];  // 记录每个深度的非叶子结点

void dfs(int u, int p, int d) {
  depth[u]        = d;
  in[u]           = ++timer;
  max_depth[u]    = d;
  bool have_child = false;

  for (auto &v : adj[u]) {
    if (v != p) {
      have_child = true;
      dfs(v, u, d + 1);
      max_depth[u] = max(max_depth[u], max_depth[v]);
    }
  }

  is_leaf[u] = !have_child;
  out[u]     = timer;
}

void solve() {
  int n;
  cin >> n;
  for (int i = 0; i < n - 1; i++) {
    int u, v;
    cin >> u >> v;
    adj[u].push_back(v);
    adj[v].push_back(u);
  }

  dfs(1, 0, 1);

  // 按深度记录非叶子结点的进入时间
  for (int i = 1; i <= n; i++) {
    if (!is_leaf[i]) {
      non_leaf_at_depth[depth[i]].push_back(in[i]);
    }
  }

  // 对每个深度的非叶子结点的进入时间进行排序
  for (int d = 1; d <= n; ++d) {
    if (!non_leaf_at_depth[d].empty()) {
      sort(non_leaf_at_depth[d].begin(), non_leaf_at_depth[d].end());
    }
  }

  for (int u = 1; u <= n; ++u) {
    if (is_leaf[u]) {
      cout << 0 << (u == n ? "" : " ");
    } else {
      int target_d     = max_depth[u] - 1;
      vector<int> &vec = non_leaf_at_depth[target_d];
      // 第一个>=in[u]的下标
      int l = lower_bound(vec.begin(), vec.end(), in[u]) - vec.begin();
      // 第一个>out[u]的下标
      int r = upper_bound(vec.begin(), vec.end(), out[u]) - vec.begin();

      cout << r - l << (u == n ? "" : " ");
    }
  }
}

signed main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);
  int t = 1;
  // cin >> t;
  while (t--) solve();
  return 0;
}
```