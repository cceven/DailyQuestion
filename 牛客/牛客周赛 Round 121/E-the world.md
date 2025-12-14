[the world](https://ac.nowcoder.com/acm/contest/124143/E)
使用BFS。并且使用思维数组记录每一个位置的状态，分别是x,y的坐标，当前时间的奇偶性，当前的技能状态。
![[Pasted image 20251214154936.png]]
```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int ll

const int MAXN = 1005;

bool bad[MAXN][MAXN][2];     // 幽灵位置
int dist[MAXN][MAXN][2][4];  // 到达该点的最短时间

struct Node {
    int x, y;
    int g;     // 当前时间状态。0:奇数秒，1:偶数秒
    int mode;  // 0(未使用),1(使用第一秒),2(使用第二秒),3(使用过了)三种状态
};

// 四个方向
int dx[] = { 0, 0, 1, -1 };
int dy[] = { 1, -1, 0, 0 };

void solve() {
  int n, m, k;
  cin >> n >> m >> k;

  // 记录幽灵出现的位置
  for (int i = 0; i < k; i++) {
    int x1, y1, x2, y2;
    cin >> x1 >> y1 >> x2 >> y2;
    bad[x1][y1][0] = true;
    bad[x2][y2][1] = true;
  }

  // dist数组初始化为1，表示未访问过
  for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= m; j++) {
      for (int g = 0; g <= 1; g++) {
        for (int mode = 0; mode <= 3; mode++) {
          dist[i][j][g][mode] = -1;
        }
      }
    }
  }

  // 开始BFS
  queue<Node> q;
  q.push({ 1, 1, 0, 0 });
  dist[1][1][0][0] = 0;

  while (!q.empty()) {
    auto &[x, y, g, mode] = q.front();
    q.pop();

    int d = dist[x][y][g][mode];
    // 到达目的地
    if (x == n && y == m) {
      cout << d << endl;
      return;
    }

    // 四个方向移动
    for (int i = 0; i < 4; i++) {
      // 计算下一个位置
      int nx = x + dx[i];
      int ny = y + dy[i];

      //--- 方案A：普通移动 ---
      if (mode == 0 || mode == 2 || mode == 3) {
        int ng    = 1 - g;
        int nmode = mode;
        // 如果没有幽灵并且没有访问过
        if (!bad[nx][ny][ng] && dist[nx][ny][ng][nmode] == -1) {
          dist[nx][ny][ng][nmode] = d + 1;
          q.push({ nx, ny, ng, nmode });
        }
      }

      //--- 方案B：技能移动----
      if (mode == 0 || mode == 1) {
        int ng    = g;
        int nmode = (mode == 0 ? 1 : 2);
        // 如果没有幽灵并且没有访问过
        if (!bad[nx][ny][ng] && dist[nx][ny][ng][nmode] == -1) {
          dist[nx][ny][ng][nmode] = d + 1;
          q.push({ nx, ny, ng, nmode });
        }
      }
    }
  }
  cout << -1 << endl;
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






