# [F.小苯的因子查询](https://ac.nowcoder.com/acm/contest/108038/F)

![image-20250508011910731](https://gitee.com/chen-houchao/images/raw/master/202505080119857.png)

## 代码

**质因数分解（唯一分解定理）**： 每个合数都可以写成几个质数相乘的形式

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int ll

const int MOD = 998244353;
int m         = 1e6;

int fastPow(int a, int b, int p) {
  int res = 1;
  a %= p;
  while (b) {
    if (b & 1) {
      res = res * a;
      res %= p;
    }

    b >>= 1;
    a = (a * a) % p;
  }
  return res % p;
}

vector<int> minp(m + 1), primes;  // 每个数的最小质因子和素数集合
vector<int> total(m + 1), odd(m + 1), inv(m + 1), d(m + 1);

void solve() {
  // 找到每个数的最小质因子和素数集合
  for (int i = 2; i <= m; i++) {
    // 当前为素数
    if (!minp[i]) {
      minp[i] = i;          // 素数的最小质因子为自身
      primes.push_back(i);  // 添加到素数集合
    }

    for (auto &p : primes) {
      if (i * p > m) break;  // 如果越界了，直接break
      minp[i * p] = p;
      // 后面的都是i*num的形式，如果minp[i]==p，那么后面的最小质因子肯定小于等于p
      if (p == minp[i]) break;
    }
  }

  // 找到所有数的逆元（线性求逆元）
  inv[1] = 1;
  for (int i = 2; i <= m; i++) {
    inv[i] = (MOD - MOD / i) * inv[MOD % i] % MOD;
  }

  total[0] = odd[0] = 1;
  for (int i = 1; i <= m; i++) {
    int j = i;
    vector<pair<int, int>> mp;
    // 找到i的所有质因子
    while (j > 1) {
      int p = minp[j];
      int k = 0;
      while (j % p == 0) {
        j /= p;
        k++;
      }
      mp.push_back({ p, k });
    }

    // 继承前面的结果
    total[i] = total[i - 1];
    odd[i]   = odd[i - 1];
    for (auto &[p, k] : mp) {
      // 除掉原来的结果
      total[i] *= inv[d[p] + 1];
      total[i] %= MOD;
      if (p != 2) {
        odd[i] *= inv[d[p] + 1];
        odd[i] %= MOD;
      }

      // 加上现在的结果
      d[p] += k;
      total[i] *= (d[p] + 1);
      total[i] %= MOD;
      if (p != 2) {
        odd[i] *= (d[p] + 1);
        odd[i] %= MOD;
      }
    }
  }
}

signed main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);
  int t = 1;
  cin >> t;
  solve();
  while (t--) {
    int x;
    cin >> x;
    cout << (odd[x] * fastPow(total[x], MOD - 2, MOD)) % MOD << " ";
  }
  return 0;
}
```

## 线性筛法

基于埃拉托斯特尼筛法的优化算法，用于高效地筛选素数和计算每个数的最小质因子。

```cpp
  // 找到每个数的最小质因子和素数集合
  for (int i = 2; i <= m; i++) {
    // 当前为素数
    if (!minp[i]) {
      minp[i] = i;          // 素数的最小质因子为自身
      primes.push_back(i);  // 添加到素数集合
    }

    for (auto &p : primes) {
      if (i * p > m) break;  // 如果越界了，直接break
      minp[i * p] = p;
      // 后面的都是i*num的形式，如果minp[i]==p，那么后面的最小质因子肯定小于等于p
      if (p == minp[i]) break;
    }
  }
```

