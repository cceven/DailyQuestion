# **L3-1 City 不 City**

分数 30

作者 陈越

单位 浙江大学

“City 不 City”因为一位外国友人保保熊直播旅游时总是用奇怪的腔调说“好 city，啊！”而走红中国社交网络，成为网络热梗。事实上，有一些叛逆的年轻人在旅行时会刻意避开网红打卡点，选择一些小众的特色地方小城镇，不追求 city，而喜欢说“好 country，啊”。
下面给定各个城镇的旅游热度和城镇间的旅行花销，请你为前来咨询的旅行者规划一条最经济的路线，并且尽可能避开热度很高的网红点。

## 输入格式：

输入第一行首先给出 4 个正整数：*n* 和 *m*（1<*n*≤103，1≤*m*≤5*n*），依次为城镇数量（于是城镇编号从 1 到 *n*）和城镇间的通路条数；*s* 和 *t* 依次为旅行者的出发地和目的地的城镇编号。
随后一行给出 *n* 个不超过 100 的正整数，依次为 *n* 个城镇的旅游热度。
再后面是 *m* 行，每行给出一条通路连接的两个城镇的编号、这条通路的最小花销（其数值为不超过 103 的正整数）。通路是双向的，题目保证任一对城镇间至多给出一条通路。
同一行的数字间均以空格分隔。

## 输出格式：

题目要求从 *s* 到 *t* 的最小花销路线；若这样的路线不唯一，则取**途径**城镇的最高旅游热度值最小的那条路线。
在一行中输出从 *s* 到 *t* 的最小花销、以及途经城镇的最高旅游热度值（若没有途经的城镇，则热度值为 0）。数值间以 1 个空格分隔，行首尾不得有多余空格。
若从 *s* 根本走不到 *t*，则在一行中输出 `Impossible`。

## 输入样例 1：

```in
8 14 7 8
100 20 30 10 50 80 100 100
7 1 1
7 2 2
7 3 1
7 4 2
1 2 1
1 5 2
2 5 1
3 4 1
3 5 3
3 6 2
4 6 1
5 6 1
5 8 1
6 8 2
```

## 输出样例 1：

```out
4 50
```

## 样例解释：

从 7 到 8 的最短路径有 3 条，其中 2 条都经过城镇 1，于是对应的最高旅游热度值是城镇 1 的热度值 100。解路径为 7->2->5->8，途径城镇 2 和 5，对应的最高旅游热度值是城镇 5 的热度值 50。在最短路径长度相等的情况下，取热度值小的解，故输出的热度值为 50。

## 输入样例 2：

```in
3 1 1 2
10 20 30
1 3 1
```

## 输出样例 2：

```out
Impossible
```

代码长度限制

16 KB

Java (javac)

时间限制

800 ms

内存限制

512 MB

其他编译器

时间限制

400 ms

内存限制

64 MB

栈限制

8192 KB

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  int n, m, s, t;
  cin >> n >> m >> s >> t;

  vector<int> hot_num(n + 1);  // 每个城镇的热度
  for (int i = 1; i <= n; i++) cin >> hot_num[i];

  vector<vector<pair<int, int>>> g(n + 1);  // 邻接表
  for (int i = 1; i <= m; i++) {
    int u, v, p;
    cin >> u >> v >> p;
    g[u].push_back({ v, p });
    g[v].push_back({ u, p });
  }

  // 优先队列：{花费，最大热度，当前节点}}
  priority_queue<
          tuple<int, int, int>, vector<tuple<int, int, int>>,
          greater<tuple<int, int, int>>>
          pq;

  vector<int> is_visit(n + 1, false);  // 标记是否已经访问过
  vector<pair<int, int >> dist(n + 1, { INT_MAX, INT_MAX });
  dist[s] = { 0, 0 };
  pq.push({ 0, 0, s });
  while (!pq.empty()) {
    auto [cur_cost, cur_hot, u] = pq.top();
    pq.pop();

    // 已经访问过了就直接跳过
    if (is_visit[u]) continue;
    is_visit[u] = true;

    for (auto [v, cost] : g[u]) {
      int new_cost = cur_cost + cost;
      int new_hot  = cur_hot;
      if (v != s && v != t) new_hot = max(cur_hot, hot_num[v]);

      if (make_pair(new_cost, new_hot) < dist[v]) {
        dist[v] = { new_cost, new_hot };
        pq.push({ new_cost, new_hot, v });
      }
    }
  }

  if (dist[t].first == INT_MAX)
    cout << "Impossible";
  else
    cout << dist[t].first << " " << dist[t].second;
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);
  int t = 1;
  // cin>>t;
  while (t--) solve();
  return 0;
}
```

