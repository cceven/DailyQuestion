#前缀和
[无穷无尽的字符串](https://ac.nowcoder.com/acm/contest/123788/B)
![[Pasted image 20251205183147.png]]
## 代码
使用**前缀和**来做本题。要求`[l, r]`之间字符串`a,b,c`的数量，即$[1, r] - [1, l - 1]$两个区间相减。而且因为求1到n的字符数量比较好求，可以直接先求有多少个3的循环，然后余1就说明`a`多了1个，余2就说明`a`和`b`多了1个。所以前缀和是本题的最优解，`for`循环可能导致时间爆炸。
```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int ll

// 统计从1到n中A,B,C出现的次数
vector<ll> countPre(ll n) {
  if (n == 0) return { 0, 0, 0 };
  int loops = n / 3;
  int rem   = n % 3;

  int countA = loops;
  int countB = loops;
  int countC = loops;

  if (rem == 1)
    countA++;
  else if (rem == 2) {
    countA++;
    countB++;
  }

  return { countA, countB, countC };
}

void solve() {
  int l, r;
  cin >> l >> r;

  vector<ll> countR = countPre(r);
  vector<ll> countL = countPre(l - 1);
  for (int i = 0; i < 3; i++) {
    cout << countR[i] - countL[i] << " ";
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