# [B.小红开灯（二）](https://ac.nowcoder.com/acm/contest/107000/B)

![image-20250414003254533](https://gitee.com/chen-houchao/images/raw/master/202504140032607.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;

void solve() {
  int n;
  cin >> n;
  int cnt = 0;  // 需要关掉的灯的数量
  string s;     // 所有的灯的状态
  cin >> s;
  for (int i = 0; i < n - 1; i++) {
    // 如果当前的灯是亮着的且后面一盏灯也是亮着的，那么关闭后面的一盏灯
    if (s[i] == '1' && s[i + 1] == '1') {
      cnt++;
      s[i + 1] = '0';
    }
  }
  // 输出最后的需要关掉的灯的数量
  cout << cnt << endl;
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);

  int t = 1;
  //	cin>>t;
  while (t--) {
    solve();
  }
  return 0;
}
```

