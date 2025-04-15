# [C.连续数组](https://ac.nowcoder.com/acm/contest/105825/C)

![image-20250402145320553](https://gitee.com/chen-houchao/images/raw/master/202504021453092.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  int q;  // 数组的个数
  cin >> q;
  // 连续数组的开始数（最小数）和结束数（最大数）
  int start_num = INT_MAX, end_num = INT_MIN;
  bool is_able = true;                // 是否有解
  unordered_map<int, bool> is_valid;  // 某个数字是否存在
  for (int i = 0; i < q; i++) {
    int k;  // 数字的数量
    cin >> k;
    int pre = -1;  // 前一个数字

    for (int j = 0; j < k; j++) {
      int cur_num;
      cin >> cur_num;
      // 如果当前数字小于等于前面的数字（即不是递增的），或者已经出现过了（重复），那么无解
      if (cur_num <= pre || is_valid[cur_num]) {
        is_able = false;
      }
      pre = cur_num;  // 更新“前一个”数字
      // 更新开始数和结束数
      start_num = min(start_num, cur_num);
      end_num   = max(end_num, cur_num);
      // 标记为出现过
      is_valid[cur_num] = true;
    }
  }

  // 如果无解，那么直接输出
  if (!is_able) {
    cout << "NO";
    return;
  }

  // 如果连续数组中有某个数字不存在，那么无解
  for (int i = start_num; i <= end_num; i++) {
    if (!is_valid[i]) {
      cout << "NO";
      return;
    }
  }
  cout << "YES";
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);
  int t = 1;
  // cin >> t;
  while (t--) solve();
  return 0;
}
```

