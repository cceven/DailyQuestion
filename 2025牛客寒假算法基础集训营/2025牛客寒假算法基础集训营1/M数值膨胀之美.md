# 数值膨胀之美

**STL**、**排序**、**枚举**

![image-20250121195305208](https://gitee.com/chen-houchao/images/raw/master/202501211953326.png)

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
    numSeq[nums[i]] = i;  // 记住数字的原始位置
  }
  sort(nums.begin(), nums.end());

  nums[0] *= 2;  // 最小的数字肯定需要乘2
  for (int i = 1; i < n; i++) {
    // 依次往上查看，如果原始序列相邻那么也要乘2，直到不相邻
    if (numSeq[nums[i]] != numSeq[nums[i - 1]] + 1) {
      break;
    }
    nums[i] *= 2;
  }

  // 区间乘2后的数据序列，求极差
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

