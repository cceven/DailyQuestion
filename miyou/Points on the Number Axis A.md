## Points on the Number Axis **A**

Alice is playing a single-player game on the number axis.

There are n*n* points on the number axis. Each time, the player selects two points. The two points will be removed, and their midpoint will be added. When there is only one point on the axis, the game ends. Formally, if the two chosen points is xi*x**i* and xj*x**j*, then xi+xj22*x**i*+*x**j* will be added after the operation.

In order to play this game happily, Alice will always select two points randomly.

Now Alice have a question: where is the expected position of the last point.

It can be proven that the answer can be expressed in the form pq*q**p*, you only need to output the value of p⋅q−1mod998244353*p*⋅*q*−1mod998244353.

### Input

The first line contains one integer n*n* (1≤n≤1061≤*n*≤106).

The second line contains n*n* integers xi*x**i* (0≤x1≤⋯≤xn<9982443530≤*x*1≤⋯≤*x**n*<998244353), denoting the position of the i*i*-th point.

Note that two points may be in the same position.

### Output

Output one integer, the answer modulo 998244353998244353.

### Examples

| Inputcopy  | Outputcopy  |
| ---------- | ----------- |
| `3 1 2 4 ` | `332748120` |

### 思路

因为每次删掉两个数字然后添加上它们的平均数，其实到最后也就相当于求所有数字的平均数。只不过加上了取模运算，因此引入了**乘法逆元**。

### 代码

#### 扩展欧几里得算法

```cpp
#include <bits/stdc++.h>
using namespace std;
using ll        = long long;
constexpr int P = 998244353;

// 扩展欧几里得算法  ax+by=gcd(a,b)
ll exgcd(ll a, ll b, ll &x, ll &y) {
  // 递归终止条件
  if (b == 0) {
    x = 1;
    y = 0;
    return a;
  }
  // 递归
  ll x1, y1, gcd;
  gcd = exgcd(b, a % b, x1, y1);
  x   = y1;
  y   = x1 - (a / b) * y1;
  return gcd;
}

// 求乘法逆元的函数
ll mod_inverse(ll a) {
  ll x, y;
  exgcd(a, P, x, y);
  return (x % P + P) % P;  // 防止返回负数
}

void solve() {
  ll n;
  cin >> n;
  vector<ll> nums(n);
  ll sum = 0;
  for (ll &num : nums) {
    cin >> num;
    sum = (sum + num) % P;
  }
  cout << (sum * mod_inverse(n)) % P << endl;
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);

  solve();
  return 0;
}

```

#### 费马小定理

```cpp
#include <bits/stdc++.h>
using namespace std;
using ll    = long long;
constexpr int P = 998244353;

// 快速幂函数，计算 base^exp % mod
ll fast_pow(ll a, ll b) {
  ll res = 1;
  while (b) {
    // 如果幂为奇数，那么要提出来一个a
    if (b & 1) {
      res = (res * a) % P;
    }
    // 底数平方，幂减一
    a = (a * a) % P;
    b >>= 1;
  }
  return res;
}

void solve() {
  ll n;
  cin >> n;
  vector<ll> nums(n);
  ll sum = 0;
  for (ll &num : nums) {
    cin >> num;
    sum = (sum + num) % P;
  }
  cout << (sum * fast_pow(n, P - 2)) % P << endl;
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);

  solve();
  return 0;
}
```

- 取模运算在有const限制下会有编译器优化
- `using`的用法