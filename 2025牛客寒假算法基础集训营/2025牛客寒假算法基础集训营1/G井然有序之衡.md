```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;

void solve() {
  long long n;
  cin >> n;
  vector<long long> nums(n);
  long long sum = 0;
  for (long long i = 0; i < n; i++) {
    cin >> nums[i];
    sum += nums[i];
  }
  if (sum != (1 + n) * n / 2) {  // 不能
    cout << "-1";
    return;
  }

  sort(nums.begin(), nums.end());
  long long ope = 0;
  for (int i = 0; i < nums.size(); i++) {
    if (nums[i] != i + 1) {
      ope += abs(nums[i] - (i + 1));
      nums[i] = i + 1;
    }
  }

  cout << ope / 2;
  return;
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);

  solve();
  return 0;
}

```

