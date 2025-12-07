[无穷无尽的数](https://ac.nowcoder.com/acm/contest/123788/F)
1. 问题转化：利用前缀相减
我们要求第 $l$ 到第 $r$ 位组成的数字的值。假设我们要截取字符串 $S$ 的中间一段 $S[l \dots r]$，它的值可以通过以下公式计算：
$$\text{Value}(l, r) = \text{Value}(1, r) - \text{Value}(1, l-1) \times 10^{(r - l + 1)}$$
所以，问题变成了：**如何快速计算无限循环字符串的前 $k$ 位组成的数值？**

2. 计算前 $k$ 位的值

无限字符串是由长度为 $n$ 的字符串 $x$ 不断循环拼接而成的。对于前 $k$ 位，我们可以把它拆分为两部分：
- **完整部分**：包含了 $q = \lfloor k / n \rfloor$ 个完整的字符串 $x$。
- **剩余部分**：包含了字符串 $x$ 的前 $rem = k \% n$ 位。
Part A: 完整部分的计算 (等比数列)
这 $q$ 个 $x$ 拼接在一起，实际上是一个等比数列求和的形式。假设 $V_x$ 是单次字符串 $x$ 的数值，$P = 10^n$ 是 $x$ 的位权偏移量。完整 $q$ 个 $x$ 的值为：
$$V_{\text{full}} = V_x \times P^{q-1} + V_x \times P^{q-2} + \dots + V_x \times 1$$
提取 $V_x$，这是一个首项为 1，公比为 $P = 10^n$，项数为 $q$ 的等比数列。利用等比数列求和公式：
$$\text{Sum} = V_x \times \frac{(10^n)^q - 1}{10^n - 1} \pmod M$$
注意：除法在模运算中等于乘以为逆元。
Part B: 剩余部分的计算
剩下的 $rem$ 位就是 $x$ 的一个前缀。我们可以在输入时预处理一个 pre 数组，pre\[rem\] 就代表 $x$ 前 $rem$ 位的值。
Part C: 组合
前 $k$ 位总值 = 完整部分的值 $\times 10^{rem} +$ 剩余部分的值。
代码如下：

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int ll

const ll MOD = 998244353;
ll n, l, r;
string x;
ll pre[100005];
ll val_x = 0;

// 快速幂
ll qpow(ll base, ll exp) {
  ll res = 1;
  while (exp > 0) {
    if (exp % 2 == 1) res = (res * base) % MOD;
    base = (base * base) % MOD;
    exp /= 2;
  }
  return res;
}

// 求逆元
ll inv(ll x) {
  return qpow(x, MOD - 2);
}

ll calc(ll k) {
  ll loops = k / n;  // 有多少个完整的数字
  ll rem   = k % n;  // 剩余多少位，从pre数组中取指

  ll ratio    = qpow(10, n);  // 公比，用于等比数列求和
  ll geom_sum = 0;

  // 等比数列求和公式
  geom_sum = val_x * (qpow(ratio, loops) - 1) % MOD *
             inv((ratio - 1 + MOD) % MOD) % MOD;
  ll total = geom_sum * qpow(10, rem) % MOD;
  total    = (total + pre[rem]) % MOD;
  return total;
}

void solve() {
  cin >> n >> l >> r;
  cin >> x;
  for (int i = 1; i <= n; i++) {
    pre[i] = (pre[i - 1] * 10 + (x[i - 1] - '0')) % MOD;
  }
  val_x = pre[n];

  ll ans_r = calc(r);
  ll ans_l = calc(l - 1);
  ll shift = r - l + 1;
  ll ans   = (ans_r - (ans_l * qpow(10, r - l + 1)) % MOD + MOD) % MOD;
  cout << ans << endl;
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







