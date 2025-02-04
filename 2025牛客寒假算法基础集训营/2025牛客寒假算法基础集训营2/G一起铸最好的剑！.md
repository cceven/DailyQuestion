# 一起铸最好的剑！

![image-20250123132824060](https://gitee.com/chen-houchao/images/raw/master/202501231328182.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;

void solve() {
  int bestTemp, powNum;
  cin >> bestTemp >> powNum;
  if (powNum == 1) {  // 如果powNum为1，无论填多少次柴都是1
    cout << "1" << endl;
    return;
  }

  long long currentTemp = powNum;                         // 当前温度
  long long bestDiff    = llabs(currentTemp - bestTemp);  // 最优的差值
  int k                 = 1;                              // 当前添加次数
  int bestK             = 1;                              // 最优的添加次数

  while (true) {
    // 先看是否溢出，原式子应为(currentTemp*powNum>LLONG_MAX)
    if (currentTemp > LLONG_MAX / powNum) {
      break;
    }

    // 再次添柴
    currentTemp *= powNum;
    k++;
    long long diff = llabs(currentTemp - bestTemp);  // 新的差值

    // 更新最优数据
    if (diff == 0) {  // 如果差值为0，一定是最优解
      bestDiff = diff;
      bestK    = k;
      break;
    }

    // 当前差值更小或者差值相同但是操作次数k更小
    if (diff < bestDiff || (diff == bestDiff && k < bestK)) {
      bestDiff = diff;
      bestK    = k;
    }

    // 之后肯定是差距越来越大，所以直接跳出循环
    if (currentTemp > bestTemp) {
      break;
    }
  }

  cout << bestK << endl;
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

