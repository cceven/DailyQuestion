# L.智乃的三角遍历

![image-20250311215745100](https://gitee.com/chen-houchao/images/raw/master/202503112157238.png)

## 代码

欧拉回路、DFS

欧拉回路，如果要保证有回路，那么每个节点的度应该都为偶数（因为要保证进去一次然后出来一次，如果起点和终点可以不同的话，那么起点和终点的度可以为奇数）

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;

vector<pair<int, int>> edges[1000];  // 存储所有的边
int num = 0;  // 存储边的序号，用于区分不同的边
unordered_map<int, bool> isVisited;  // 存储边是否访问过（边序号，是否访问过）
vector<int> ans;                     // 存储答案

void addEdge(const int &u, const int &v) {
  edges[u].emplace_back(v, num);
  edges[v].emplace_back(u, num++);
}

void dfs(const int &u) {
  for (auto &e : edges[u]) {
    // 如果这条边已经访问过了，那么直接跳过
    if (isVisited[e.second]) continue;
    // 如果没有访问过，那么进行访问
    isVisited[e.second] = true;
    // 递归
    dfs(e.first);
  }
  ans.push_back(u);
}

void solve() {
  int n;  // n层
  cin >> n;
  vector<int> startNode(n + 1);  // 存储每一层的第一个节点的值
  startNode[0] = 1;
  for (int i = 1; i <= n; i++) {
    startNode[i] = startNode[i - 1] + i;
  }

  // 开始连接边
  for (int i = 0; i < n; i++) {
    for (int j = 0; j <= i; j++) {
      int p1 = startNode[i] + j, p2 = startNode[i + 1] + j,
          p3 = startNode[i + 1] + j + 1;
      addEdge(p1, p2);
      addEdge(p1, p3);
      addEdge(p2, p3);
    }
  }
  // 进行深度优先遍历
  dfs(1);
  // 开始输出
  cout << "Yes" << endl;
  for (int i = 0; i < ans.size(); i++) {
    if (i) cout << " ";
    cout << ans[i];
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

