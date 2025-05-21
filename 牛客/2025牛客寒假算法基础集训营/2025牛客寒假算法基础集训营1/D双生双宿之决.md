# 双生双宿之决

**模拟**、**排序**

![image-20250121194517464](https://gitee.com/chen-houchao/images/raw/master/202501211945578.png)

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;

void solve() {
  int n;
  cin >> n;

  vector<int> nums(n);
  unordered_set<int> freq;  // 用于查看有多少种数据，确保为两种
  for (int i = 0; i < n; i++) {
    cin >> nums[i];
    freq.insert(nums[i]);
  }
  // 如果数据个数为奇数个或者数据的种类不为两种，那么就No
  if (n % 2 != 0 || freq.size() != 2) {
    cout << "No" << endl;
    return;
  }

  sort(nums.begin(), nums.end());
  // 第二种数据的第一个数据的位置，用二分查找
  auto secFir = upper_bound(nums.begin(), nums.end(), nums[0]) - nums.begin();
  if (secFir != ceil(n / 2)) {  // 如果不是刚好一半的位置
    cout << "No" << endl;
  } else {  // 刚好在一半的位置，符合要求
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

