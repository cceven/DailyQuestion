# 井然有序之衡

**思维**、**排序**

![image-20250121194951073](https://gitee.com/chen-houchao/images/raw/master/202501211949192.png)

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;

void solve() {
  long long n;
  cin >> n;
  vector<long long> nums(n);
  long long sum = 0;  // 数据和
  for (long long i = 0; i < n; i++) {
    cin >> nums[i];
    sum += nums[i];
  }  // 如果所有的数据和不符合要求，那么无论怎么操作都不行
  if (sum != (1 + n) * n / 2) {
    cout << "-1";
    return;
  }

  sort(nums.begin(), nums.end());
  long long ope = 0;  // 操作的次数
  for (int i = 0; i < nums.size(); i++) {
    if (nums[i] != i + 1) {  // 当前数据需要操作
      // 操作数，最后需要除以2，因为两边同时操作，这里分开算了
      ope += abs(nums[i] - (i + 1));
      nums[i] = i + 1;  // 操作后符合要求
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

