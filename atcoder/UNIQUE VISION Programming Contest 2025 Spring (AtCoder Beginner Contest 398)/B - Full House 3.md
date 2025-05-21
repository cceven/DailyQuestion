# [**B - Full House 3**](https://atcoder.jp/contests/abc398/tasks/abc398_b)

![image-20250401235733673](https://gitee.com/chen-houchao/images/raw/master/202504012357829.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  unordered_set<int> cards;     // 不同的卡牌种类
  unordered_map<int, int> cnt;  // 不同的卡牌出现的次数
  // 开始输入卡牌
  for (int i = 0; i < 7; i++) {
    int cur_card;
    cin >> cur_card;
    cards.insert(cur_card);
    cnt[cur_card]++;
  }

  // 分别代表是否有可以拿出两个和三个的
  bool is_two = false, is_three = false;
  for (auto it = cards.begin(); it != cards.end(); it++) {
    // 这里要首先判断可以拿出三个的，不然可能让三个的归类到了两个的那一类
    if (cnt[*it] >= 3) {
      // 如果已经有可以拿出三个的了，那么这次的拿出两个
      if (is_three == true) is_two = true;
      // 可以拿出三个
      is_three = true;
    } else if (cnt[*it] >= 2) {
      // 可以拿出两个
      is_two = true;
    }
  }

  // 输出答案
  if (is_two && is_three) {
    cout << "Yes";
  } else {
    cout << "No";
  }
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

