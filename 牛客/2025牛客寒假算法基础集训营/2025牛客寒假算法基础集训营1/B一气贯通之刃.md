# 一气贯通之刃

**图论**

![image-20250121193822177](https://gitee.com/chen-houchao/images/raw/master/202501211938299.png)

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;

void solve() {
  int n;
  cin >> n;
  unordered_map<int, int> mp;  // 存储每个点的度数
  for (int i = 0; i < n - 1; i++) {
    int x, y;
    cin >> x >> y;
    mp[x]++;
    mp[y]++;
  }

  vector<int> ans;
  for (int i = 1; i <= n; i++) {
    if (mp[i] == 1) {  // 度数为1的就符合要求
      ans.push_back(i);
    }
  }

  if (ans.size() != 2) {  // 如果不是只有两个点的度数为1，那么说明肯定不符合要求
    cout << "-1";
  } else {
    cout << ans[0] << " " << ans[1];  // 两个度数为1的点就是目标点
  }
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);

  solve();
  return 0;
}
```

