# **7-32 I Love GPLT**

分数 5

作者 陈越

单位 浙江大学

这道超级简单的题目没有任何输入。

你只需要把这句很重要的话 —— `I Love GPLT` ——竖着输出就可以了。

所谓“竖着输出”，是指每个字符占一行（包括空格），即每行只能有1个字符和回车。

代码长度限制

16 KB

时间限制

400 ms

内存限制

64 MB

栈限制

8192 KB

## 代码

![image-20250123113507807](https://gitee.com/chen-houchao/images/raw/master/202501231135836.png)

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;

void solve() {
  string s = "I Love GPLT";
  for (auto &c : s) {
    cout << c << endl;
  }
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);

  solve();
  return 0;
}
```

