# E-小苯的数字变换

![image-20250927194358043](https://gitee.com/chen-houchao/images/raw/master/202509271943235.png)

## 代码

​	首先需要知道一个性质，对正整数 v，dr(v) = 1 + ((v - 1) mod 9)，等价于：

- v = 0 时，dr(0) = 0
- v > 0 时，dr(v) = (v mod 9)，若 v mod 9 = 0 则为 9

​	回到这道题中，总共有三个变量需要维护：

- 计算 SumRm：
  - 前缀和 P[i] = (P[i-1] + digit[i]) mod 9
  - 维护出现过的前缀余数计数 cnt[0..8]（含空前缀 cnt[0]=1）
  - 固定右端 i，所有左端 j 的子串余数是 (P[i] - P[j]) mod 9
  - 本次贡献是 sum_{r=0..8} ((P[i] - r + 9) % 9) * cnt[r]
- 计算 C9：
  - 每次 i，使 C9 += cnt[P[i]]（因为要余 0，需左端前缀余数与 P[i] 相同）
- 计算 Z：
  - 统计 0 连续段长度 L，贡献 L*(L+1)/2，累加即可

```cpp
#include <bits/stdc++.h>
#define endl "\n"
#define int  long long
using namespace std;
 
void solve() {
  string x;
  cin >> x;
  const int MOD = 9;
  int cnt[MOD]  = { 0 };  // cnt[r]表示前缀和对9取模为r的数k量
 
  int SumRm = 0;  // 所有子串对9取模和
  int C9    = 0;  // 9的数量
  int Z     = 0;  // 0串的数量
 
  // 计算0串的数量
  {
    int run = 0;
    for (char c : x) {
      if (c == '0')
        run++;
      else {
        if (run) Z += (run * (run + 1)) / 2;
        run = 0;
      }
    }
    if (run) Z += (run * (run + 1)) / 2;
  }
 
  int p  = 0;  // 当前的前缀和对9取模的值，也就是p[i]
  cnt[0] = 1;  // 空串
  for (char c : x) {
    int d = c - '0';
    p += d;  // 当前的p[i]
    p %= MOD;
 
    int localContri = 0;
    for (int r = 0; r < MOD; r++) {
      int t = (p - r + MOD) % MOD;  // p[i]-p[j]
      localContri += cnt[r] * t;
    }
 
    SumRm += localContri;
 
    C9 += cnt[p];  // p[i]==p[j]
 
    cnt[p]++;
  }
 
  int ans = SumRm + 9LL * (C9 - Z);
  cout << ans << endl;
}
 
signed main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);
  int t = 1;
  cin >> t;
  while (t--) solve();
  return 0;
}
```

