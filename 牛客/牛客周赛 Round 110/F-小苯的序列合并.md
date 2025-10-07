# F-小苯的序列合并

![image-20250927194719534](https://gitee.com/chen-houchao/images/raw/master/202509271947636.png)

## 代码

​	首先需要知道，这道题最好的分段情况肯定是不超过2段。因为如果能异或的情况下肯定要使得尽量多的数字进行异或来使得有尽可能多的1。

​	如果最后异或到只剩下两段数字，那么直接遍历找到最大值就可以了。

```cpp
#include <bits/stdc++.h>
#define endl "\n"
#define int  long long
using namespace std;
 
void solve() {
  int n;
  cin >> n;
  vector<int> a(n + 1);
  vector<int> pre(n + 2, 0);  // 异或前缀和
  for (int i = 1; i <= n; i++) {
    cin >> a[i];
    pre[i] = pre[i - 1] ^ a[i];
  }
 
  int ans = pre[n];  // 全部xor为一段的情况
  int suf = 0;
  for (int i = n ; i > 0; i--) {  // 两段的情况
    suf ^= a[i];
    ans = max(ans, suf & pre[i - 1]);
  }
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

