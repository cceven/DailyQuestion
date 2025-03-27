## [L.Tokitsukaze and XOR-Triangle](https://ac.nowcoder.com/acm/contest/95336/L)

![image-20250323180356415](https://gitee.com/chen-houchao/images/raw/master/202503231803512.png)

## 代码

![image-20250323180441611](https://gitee.com/chen-houchao/images/raw/master/202503231804644.png)

![image-20250323180512056](https://gitee.com/chen-houchao/images/raw/master/202503231805206.png)

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

const int MOD = 1e9 + 7;
// 大数组开在全局使用堆，防止栈爆炸
ll a_bit[300001][32][2] = { 0 }, b_bit[300001][32][2] = { 0 };
// 记录每一行的值
ll sum[300001] = { 0 };

void solve() {
  int n, q;  // 输入元素数量和询问次数
  cin >> n >> q;

  // 首先输入a数组和b数组的值
  vector<ll> a(n + 1, 0), b(n + 1, 0);
  for (int i = 1; i <= n; i++) cin >> a[i];
  for (int i = 1; i <= n; i++) cin >> b[i];

  // 储存前i个数字的第j位的k的个数
  for (int i = 1; i <= n; i++) {
    for (int j = 0; j <= 31; j++) {
      for (int k = 0; k <= 1; k++) {
        a_bit[i][j][k] = a_bit[i - 1][j][k];
        b_bit[i][j][k] = b_bit[i - 1][j][k];
      }
      a_bit[i][j][(a[i] >> j) & 1]++;
      b_bit[i][j][(b[i] >> j) & 1]++;
    }
  }

  // 开始计算每一行的值
  for (int i = 1; i <= n; i++) {
    sum[i] = sum[i - 1];  // 由于计算的是前缀和，所以要加上前一个
    for (int j = 0; j <= 31; j++) {
      int s     = (a[i] >> j) & 1;  // 当前位的值
      ll contri = (1LL << j);       // 当前位的贡献
      sum[i] += contri * (b_bit[n][j][s ^ 1] - b_bit[i - 1][j][s ^ 1]);
    }
    sum[i] %= MOD;
  }

  while (q--) {
    int l, r;  // 查询的边界
    cin >> l >> r;
    // 首先得到目标梯形包含的值
    ll ans = (sum[r] - sum[l - 1] + MOD) % MOD;

    // 减去多余的长方形部分
    for (int i = 0; i <= 31; i++) {
      ll temp = 0;
      temp += (1LL << i) * (a_bit[r][i][0] - a_bit[l - 1][i][0]) *
              (b_bit[n][i][1] - b_bit[r][i][1]);
      temp += (1LL << i) * (a_bit[r][i][1] - a_bit[l - 1][i][1]) *
              (b_bit[n][i][0] - b_bit[r][i][0]);
      temp %= MOD;
      ans -= temp;
      ans %= MOD;
    }
    if (ans < 0) ans += MOD;
    cout << ans << endl;
  }
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

