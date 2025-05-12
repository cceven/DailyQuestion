# B.token

![image-20250506233223522](https://gitee.com/chen-houchao/images/raw/master/202505062332663.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int ll

void solve() {
  int n;
  cin >> n;
  vector<int> toks(n);
  for (int i = 0; i < n; i++) {
    cin >> toks[i];
  }
  // 如果总的对话数量不大于10，那么直接输入总和
  if (n <= 10) {
    cout << reduce(toks.begin(), toks.end(), 0LL) << endl;
    return;
  }

  // 如何对话数量大于10，那么需要找到最大值
  int cur_tok = reduce(toks.begin(), toks.begin() + 10, 0LL);
  int max_tok = cur_tok;
  for (int i = 10; i < n; i++) {
    cur_tok = cur_tok + toks[i] - toks[i - 10];
    max_tok = max(max_tok, cur_tok);
  }
  cout << max_tok << endl;
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

