# [E.小苯的数组构造](https://ac.nowcoder.com/acm/contest/105623/E)

![image-20250330233301725](https://gitee.com/chen-houchao/images/raw/master/202503302333825.png)

## 代码

[题解](https://www.bilibili.com/video/BV1rvZNYqETt?spm_id_from=333.788.videopod.episodes&vd_source=d00bc79c7901f27a447b550b4ddaec3c&p=4)

![image-20250330233337767](https://gitee.com/chen-houchao/images/raw/master/202503302333805.png)

### 代码1

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  int n, x, y;
  cin >> n >> x >> y;
  // 首先y必须是x的子集
  if ((x & y) != y) {
    cout << "NO" << endl;
    return;
  }
  // 从最高位开始进行遍历
  vector<int> ans(n + 1);  // 答案
  int skip_num = 1;        // 需要跳过的数的索引
  for (int i = 31; i >= 0; i--) {
    // 提取x和y的当前位
    int a = ((x >> i) & 1), b = ((y >> i) & 1);
    // 如果x的当前位是1，那么不用计算直接跳过
    if (a == 0) continue;

    int no_skip = (a ^ b) ^ (n & 1);  // 数学归纳出来的
    if (no_skip == 0) {
      for (int j = 1; j <= n; j++) {
        if (j == skip_num) continue;
        ans[j] |= (1LL << i);
      }
      skip_num = min(skip_num + 1, n);
    } else {
      for (int j = 1; j <= n; j++) {
        ans[j] |= (1LL << i);
      }
    }
  }

  // 判断是否有0
  for (int i = 1; i <= n; i++) {
    if (ans[i] == 0) {
      cout << "NO" << endl;
      return;
    }
  }

  // 判断是否满足要求
  int res1 = 0, res2 = 0;
  for (int i = 1; i <= n; i++) {
    res1 |= ans[i];
    res2 ^= ans[i];
  }

  if (res1 != x || res2 != y) {
    cout << "NO" << endl;
  } else {
    cout << "YES" << endl;
    for (int i = 1; i <= n; i++) {
      cout << ans[i] << " ";
    }
    cout << endl;
  }
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

### 代码2

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  int n, x, y;
  cin >> n >> x >> y;
  // 首先y必须是x的子集
  if ((x & y) != y || (n == 1 && x != y)) {
    cout << "NO" << endl;
    return;
  }
  // 从最高位开始进行遍历
  vector<int> ans(n + 1);  // 答案
  int skip_num = 1;        // 需要跳过的数的索引
  for (int i = 30; i >= 0; i--) {
    // 提取x和y的当前位
    int a = ((x >> i) & 1), b = ((y >> i) & 1);
    // 如果x的当前位是1，那么不用计算直接跳过
    if (a == 0) continue;

    int no_skip = (a ^ b) ^ (n & 1);  // 数学归纳出来的
    if (no_skip == 0) {
      for (int j = 1; j <= n; j++) {
        if (j == skip_num) continue;
        ans[j] |= (1LL << i);
      }
      skip_num = min(skip_num + 1, n);
    } else {
      for (int j = 1; j <= n; j++) {
        ans[j] |= (1LL << i);
      }
    }
  }

  // 判断是否有0
  for (int i = 1; i <= n; i++) {
    if (ans[i] == 0) {
      cout << "NO" << endl;
      return;
    }
  }

  // 输出结果
  cout << "YES" << endl;
  for (int i = 1; i <= n; i++) {
    cout << ans[i] << " ";
    cout << endl;
  }
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

### 为什么会有负数？

![image-20250330233437085](https://gitee.com/chen-houchao/images/raw/master/202503302334118.png)

​	这里其实不是判断是否有负数，判断的是是否有0（题目要求的是全正数组），如果有0就不符合要求，改为下面的代码依然可以AC

![image-20250331085541877](https://gitee.com/chen-houchao/images/raw/master/202503310855922.png)

### 为什么会不符合要求？

![image-20250330233450784](https://gitee.com/chen-houchao/images/raw/master/202503302334840.png)

​	这里处理的其实是当n == 1的情况，比如输入`1 3 1`，本来应该输出`NO`，但是如果这里不进行判定的话就会输出`YES`。所以可以等效一下在前面特判一下`(n == 1) && (x != y)`，如果为`true`，那么无解直接输出`NO`，这样后面就不用进行`ans`或和异或的结果判断。

![image-20250331095155434](https://gitee.com/chen-houchao/images/raw/master/202503310951512.png)