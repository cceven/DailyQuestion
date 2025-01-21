```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;

void solve() {
  int n;
  cin >> n;
  vector<int> nums(n);
  unordered_map<int, int> numSeq;
  for (int i = 0; i < n; i++) {
    cin >> nums[i];
    numSeq[nums[i]] = i;
  }
  sort(nums.begin(), nums.end());

  nums[0] *= 2;
  for (int i = 1; i < n; i++) {
    if (numSeq[nums[i]] != numSeq[nums[i - 1]] + 1) {
      break;
    }
    nums[i] *= 2;
  }
  sort(nums.begin(), nums.end());
  cout << nums[n - 1] - nums[0] << endl;
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);

  solve();
  return 0;
}

```

