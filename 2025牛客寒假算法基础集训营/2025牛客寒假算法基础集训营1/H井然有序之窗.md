# 井然有序之窗

![image-20250123013019309](https://gitee.com/chen-houchao/images/raw/master/202501230130426.png)

## 代码

**构造**、**贪心**

![image-20250123013108949](https://gitee.com/chen-houchao/images/raw/master/202501230131973.png)

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;

void solve() {
  int n;
  cin >> n;
  // 初始化数据
  // 存储原始的数据（左边界，右边界，原始位置）
  deque<array<int, 3>> originNums(n);
  for (int i = 1; i <= n; i++) {
    int l, r;
    cin >> l >> r;
    originNums[i - 1] = { l, r, i };
  }
  sort(originNums.begin(), originNums.end());  // 按照左边界进行排序

  vector<int> ans(n + 1);           // 存储最后的答案
  set<array<int, 3>> nowAvailable;  // 当前可用的数（左边界小于当前位置）
  for (int i = 1; i <= n; i++) {
    // 原始数据还有剩余，当前左边界最小的点的左边界符合要求是可用的
    while (originNums.size() && originNums[0][0] <= i) {
      nowAvailable.insert({ originNums[0][1], originNums[0][0],
                            originNums[0][2] });
      originNums.pop_front();
    }

    // 没有符合要求的数
    if (!nowAvailable.size()) {
      cout << "-1";
      return;
    }

    // 取出左边界符合要求且右边界最小的数，选定位置
    auto [r, l, index] = *nowAvailable.begin();
    nowAvailable.erase(nowAvailable.begin());
    if (r < i) {
      cout << "-1";
      return;
    }

    ans[index] = i;
  }
  // 输出答案
  for (int i = 1; i <= n; i++) {
    cout << ans[i] << " ";
  }
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);

  solve();
  return 0;
}
```

- `deque`双端队列
- `array<>`
- `set`自动排序
