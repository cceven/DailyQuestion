# 硝基甲苯之袭

![image-20250205121839384](https://gitee.com/chen-houchao/images/raw/master/202502051218511.png)

## 代码

![image-20250205121915360](https://gitee.com/chen-houchao/images/raw/master/202502051219389.png)

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;

void solve() {
  int n;
  cin >> n;
  vector<int> nums(2e5 + 1, 0);  // 存储各个数字出现的次数
  for (int i = 0; i < n; i++) {
    int temp;
    cin >> temp;
    nums[temp]++;  // 出现的次数加1
  }

  ll ans = 0;  // 最终结果

  // 计算两个数字是否符合要求，符合要求的话ans增加对应的个数
  auto get = [&](int x, int y) {
    if (gcd(x, y) == (x ^ y)) {
      ans += 1LL * nums[x] * nums[y];
    }
  };

  // 遍历第一个数字
  for (int i = 1; i <= 2e5; i++) {
    // 如果第一个数字出现的次数为0，那么就直接跳过
    if (nums[i] == 0) continue;

    // 便利第一个数字的因数
    for (int j = 1; j * j <= i; j++) {
      // 如果不为因数那么直接跳过
      if (i % j != 0) continue;

      // 因数j满足那么i/j也满足
      int t1 = j;
      int t2 = i / j;

      // y1=i^t1的情况
      int y1 = i ^ t1;
      if ((y1 >= 1) && (y1 <= 2e5) && (gcd(i, y1) == t1)) {
        get(i, y1);
      }

      // y2=i^t2的情况
      if (t1 == t2) continue;
      int y2 = i ^ t2;
      if ((y2 >= 1) && (y2 <= 2e5) && (gcd(i, y2) == t2)) {
        get(i, y2);
      }
    }
  }
  cout << ans / 2;
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);

  solve();
  return 0;
}
```

- `[&]`表示以引用访问外部变量
- 找到一个数`num`的所有因子：遍历1到$\sqrt{num}$，同时如果`i`是`num`的因子，那么`num/i`也是`num`的因子，注意`i`和`num/i`有可能相同，避免重复计算

## 思路

![image-20250205121947758](https://gitee.com/chen-houchao/images/raw/master/202502051219108.png)