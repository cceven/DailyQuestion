# D. Tree Jumps

time limit per test: 2 seconds

memory limit per test: 512 megabytes

input: standard input

output: standard output

You are given a rooted tree, consisting of $n$ vertices. The vertices in the tree are numbered from $1$ to $n$, and the root is the vertex $1$. Let $d_x$ be the distance (the number of edges on the shortest path) from the root to the vertex $x$.

There is a chip that is initially placed at the root. You can perform the following operation as many times as you want (possibly zero):

-   move the chip from the current vertex $v$ to a vertex $u$ such that $d_u = d_v + 1$. If $v$ is the root, you can choose any vertex $u$ meeting this constraint; however, if $v$ is not the root, $u$ should not be a neighbor of $v$ (there should be no edge connecting $v$ and $u$).

![](https://gitee.com/chen-houchao/images/raw/master/img/20250228201551179.png)

For example, in the tree above, the following chip moves are possible: $1 \rightarrow 2$, $1 \rightarrow 5$, $2 \rightarrow 7$, $5 \rightarrow 3$, $5 \rightarrow 4$, $3 \rightarrow 6$, $7 \rightarrow 6$.

A sequence of vertices is **valid** if you can move the chip in such a way that it visits all vertices from the sequence (and only them), in the order they are given in the sequence.

Your task is to calculate the number of valid vertex sequences. Since the answer might be large, print it modulo $998244353$.

## **Input**

The first line contains a single integer $t$ ($1 \le t \le 10^4$) — the number of test cases.

The first line of each test case contains a single integer $n$ ($2 \le n \le 3 \cdot 10^5$).

The second line contains $n-1$ integers $p_2, p_3, \dots, p_n$ ($1 \le p_i &lt; i$), where $p_i$ is the parent of the $i$\-th vertex in the tree. Vertex $1$ is the root.

Additional constraint on the input: the sum of $n$ over all test cases doesn't exceed $3 \cdot 10^5$.

## **Output**

For each test case, print a single integer — the number of valid vertex sequences, taken modulo $998244353$.

## Example

### Input

```
3
4
1 2 1
3
1 2
7
1 2 2 1 4 5
```

### Output

```
4
2
8
```

### Note

In the first example, the following sequences are valid: [1][1], [1,2][1,2], [1,4][1,4], [1,4,3][1,4,3].

In the second example, the following sequences are valid: [1][1], [1,2][1,2].

In the third example, the following sequences are valid: [1][1], [1,2][1,2], [1,2,7][1,2,7], [1,2,7,6][1,2,7,6], [1,5][1,5], [1,5,3][1,5,3], [1,5,3,6][1,5,3,6], [1,5,4][1,5,4].

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;

const int MOD = 998244353;

// 加法取模
ll addMod(ll a, ll b) {
  return (a + b) % MOD;
}

// 减法取模
ll subMod(ll a, ll b) {
  return (a - b + MOD) % MOD;
}

void solve() {
  int n;  // 节点数量
  cin >> n;
  vector<vector<int>> adj(n + 1);  // 邻接矩阵，存储某个节点的所有子结点
  vector<int> par(n + 1);  // 存储每个节点的父节点
  for (int i = 2; i <= n; i++) {
    int parNode;  // 输入父节点
    cin >> parNode;
    adj[parNode].push_back(i);  // 存入子结点到其父节点的邻接矩阵
    par[i] = parNode;           // 记录父节点
  }

  // 节点存储完毕，现在开始计算每个节点的深度
  vector<int> depth(n + 1, 0);
  depth[1] = 1;                           // 根节点的深度为1
  vector<vector<int>> depthNodes(n + 1);  // 存储每种深度的所有节点
  int maxDepth = 1;
  // lambda函数的递归调用知识
  auto dfs = [&](auto self, int node) -> void {
    depthNodes[depth[node]].push_back(node);
    for (auto child : adj[node]) {
      depth[child] = depth[node] + 1;
      maxDepth     = max(maxDepth, depth[child]);
      self(self, child);
    }
  };
  dfs(dfs, 1);

  // 解决完了所有节点的深度问题
  vector<ll> f(n + 1);  // 存储到每个节点为止的答案数量
  ll sum = 0;           // 每一层的答案数量
  for (auto u : adj[1]) {
    f[u] = 1;
    sum = addMod(sum, 1);  // 根节点的每一个子结点为答案增加一个
  }
  ll ans = addMod(sum, 1);

  for (ll i = 3; i <= maxDepth; i++) {
    ll temp = 0;  // 存储这一层的答案数量和
    for (auto u : depthNodes[i]) {
      f[u] = subMod(sum, f[par[u]]);  // 去除掉父节点的影响
      temp = addMod(temp, f[u]);
    }
    sum = temp;  // 更新sum为当前这一深度的sum
    ans = addMod(ans, sum);
  }
  cout << ans << endl;
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);
  int t;
  cin >> t;
  while (t--) solve();
  return 0;
}
```

- `lambda`函数的递归调用需要注意。1.需要加上`auto self`等提前声明。2.显示指定返回类型`-> void`。详细写法见图

  ![image-20250228201802155](https://gitee.com/chen-houchao/images/raw/master/img/20250228201802250.png)