```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;

void solve() {
  int n;
  cin >> n;

  vector<int> nums(n);
  unordered_set<int> freq;
  for (int i = 0; i < n; i++) {
    cin >> nums[i];
    freq.insert(nums[i]);
  }

  if (n % 2 != 0 || freq.size() != 2) {
    cout << "No" << endl;
    return;
  }

  sort(nums.begin(), nums.end());

  auto secFir = upper_bound(nums.begin(), nums.end(), nums[0]) - nums.begin();
  if (secFir != ceil(n / 2)) {
    cout << "No" << endl;
  } else {
    cout << "Yes" << endl;
  }
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

