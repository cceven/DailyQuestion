## A.复制鸡

![image-20250328134505025](https://gitee.com/chen-houchao/images/raw/master/202503281345150.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  int n;
  cin >> n;
  vector<int> b;
  for (int i = 0; i < n; i++) {
    int num;
    cin >> num;
    // 去除掉前面所有相同的数
    while (!b.empty() && b.back() == num) {
      b.pop_back();
    }
    // 插入当前的数
    b.emplace_back(num);
  }
  cout << b.size() << endl;
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);
  int t = 1;
  cin >> t;
  while (t--) solve();
  return 0;
}
```

