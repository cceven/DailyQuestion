# 双生双宿之错

![image-20250122234346513](https://gitee.com/chen-houchao/images/raw/master/202501222343645.png)

## 代码

**思维**、**贪心**、**三分**、**排序**

![image-20250122235352289](https://gitee.com/chen-houchao/images/raw/master/202501222353314.png)

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;

void solve() {
  int n;
  cin >> n;
  vector<int> a(n + 1);
  for (int i = 1; i <= n; i++) {
    cin >> a[i];
  }
  sort(a.begin(), a.end());  // 对原始数据进行排序

  // 知道两种元素的值，求这两种元素对应的操作次数
  auto getAns = [&](const int &x, const int &y) {
    long long ans = 0;
    // 前半部分
    for (int i = 1; i <= n >> 1; i++) {
      ans += abs(a[i] - x);
    }
    // 后半部分
    for (int i = (n >> 1) + 1; i <= n; i++) {
      ans += abs(a[i] - y);
    }
    return ans;
  };

  // 需要判断两种元素是否相等，如果不相等直接返回结果，相等就需要进一步处理
  auto check = [&](const int &posX, const int &posY) {
    long long ope = 0;
    if (a[posX] != a[posY]) {  // 不相等直接返回结果
      ope = getAns(a[posX], a[posY]);
    } else {  // 相等的话，左边的减一或右边的加一，取这两种方式的最小值
      ope = min(getAns(a[posX] - 1, a[posY]), getAns(a[posX], a[posY] + 1));
    }
    return ope;
  };

  int half = n >> 1;
  int x, y;
  // 下面的两种都是操作数最小的情况
  // 奇数个，两边各取中位数
  // 偶数个，左边取左中位数，右边取右中位数
  if (half & 1) {  // 如果两边的元素个数都为奇数
                   // 奇数个，直接取中位数
    x = (half + 1) >> 1;
    y = half + x;
  } else {  // 如果两边的元素个数都为偶数
            // 偶数个，左边取左中位数，右边取右中位数
    x = half >> 1;
    y = half + x + 1;
  }
  cout << check(x, y) << endl;
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

- `lambda`函数
- `\>\>1`用来表示除以2，性能优于直接除以2，但是只能用于整数
- 中位数相关知识、左中位数、右中位数
