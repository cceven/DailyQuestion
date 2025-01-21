```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;

void solve() {
  int n;
  cin >> n;
  vector<int> nums(n);
  for (int i = 0; i < n; i++) {
    cin >> nums[i];
  }
  sort(nums.begin(), nums.end());
  if (nums[0] == 1) {
    cout << -1 << endl;
    return;
  }
  cout << "1000000007" << endl;
  return;
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);
  int T;
  cin >> T;
  while (T--) solve();
  return 0;
}
```

