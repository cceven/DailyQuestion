[三妖精say subsequence ！！！](https://ac.nowcoder.com/acm/contest/124143/C)
![[Pasted image 20251214135517.png]]
```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int ll

void solve() {
  int n;
  string s;
  cin >> n >> s;
  const int MOD = 998244353;

  unordered_map<int, int> al_cnt;  // 统计每一个字母出现的次数
  for (auto &c : s) al_cnt[c - 'a']++;

  int ans = 0;
  for (int i = 0; i < 26; i++) {
    // 选取第一个字母
    int cnt1 = al_cnt[i];
    for (int j = 0; j < 26; j++) {
      // 选取第二个字母
      if (i == j) continue;
      int cnt2 = (al_cnt[i] * al_cnt[j]) % MOD;
      for (int k = 0; k < 26; k++) {
        // 选取第三个字母
        if (k == i || k == j) continue;
        int cnt3 = (cnt2 * al_cnt[k]) % MOD;
        // 更新答案
        ans = (ans + cnt3) % MOD;
      }
    }
  }
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