# [F.回响](https://ac.nowcoder.com/acm/contest/106318/F)

![image-20250414231838442](https://gitee.com/chen-houchao/images/raw/master/202504142318602.png)

## 代码

```cpp
#include <bits/stdc++.h>
using namespace std;

void solve() {
  int n;
  cin >> n;

  vector<int> a(n);
  for (auto &x : a) cin >> x;

  // 如果首位是0
  int j = 0;  // 第一个非0的元素
  if (a[0] == 0) {
    // 找到第一个非0元素
    while (j < n && a[j] == 0) j++;

    if (j == n) {
      // 如果全部都是0
      for (int i = 1; i <= n; i++) cout << i << " ";
      return;
    } else {
      // 处理最前面的一部分0，从最后一个0开始处理
      for (int i = j - 1; i >= 0; i--) {
        if (a[i + 1] > 1)
          a[i] = a[i + 1] - 1;
        else
          a[i] = a[i + 1] + 1;
      }
    }
  }

  bool is_process = false;  // 是否正在处理一个0区间
  int r           = 0;      // 0区间的右端点
  // 处理剩余情况
  for (int l = j; l < n; l++) {
    if (a[l] != 0) {
      is_process = false;
    } else {
      // 代表一个区间的开始
      if (!is_process) {
        r = l;
        while (r < n && a[r] == 0) r++;
        is_process = true;
      }

      if (r < n && a[l - 1] > a[r])
        a[l] = a[l - 1] - 1;
      else
        a[l] = a[l - 1] + 1;
    }
  }

  // 如果构造的不符合条件，输出-1
  for (int i = 0; i < n - 1; i++) {
    if (abs(a[i] - a[i + 1]) != 1) {
      cout << "-1" << endl;
      return;
    }
  }

  // 输出答案
  for (int i = 0; i < n; i++) {
    cout << a[i] << " ";
  }
}

int main() {
  int t = 1;
  //	cin>>t;
  while (t--) {
    solve();
  }
  return 0;
}
```

