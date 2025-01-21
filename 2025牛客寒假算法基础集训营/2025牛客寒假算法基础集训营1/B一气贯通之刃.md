```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;

void solve() {
  int n;
  cin >> n;
  unordered_map<int, int> mp;
  for (int i = 0; i < n - 1; i++) {
    int x, y;
    cin >> x >> y;
    mp[x]++;
    mp[y]++;
  }

  vector<int> ans;
  for (int i = 1; i <= n; i++) {
    if (mp[i] == 1) {
      ans.push_back(i);
    }
  }

  if (ans.size() != 2) {
    cout << "-1";
  } else {
    cout << ans[0] << " " << ans[1];
  }
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);

  solve();
  return 0;
}
```

