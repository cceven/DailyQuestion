# 数据时间？

![image-20250123143218919](https://gitee.com/chen-houchao/images/raw/master/202501231432057.png)

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;

void solve() {
  int n, h, m;
  cin >> n >> h >> m;
  // 存储目标三个时间段的用户数量，使用set防止用户重复
  unordered_set<string> commuteUsers, lunchUsers, sleepUsers;

  while (n--) {
    string user_id, user_date, user_time;
    cin >> user_id >> user_date >> user_time;

    // 首先提取年月，如果不是我们要查询的那么直接跳过
    int year  = stoi(user_date.substr(0, 4));
    int month = stoi(user_date.substr(5, 2));
    if (year != h || month != m) {
      continue;
    }

    // 是我们要查询的年月，那么就提取时间，判断是哪个时间段的用户
    int hours        = stoi(user_time.substr(0, 2));
    int minutes      = stoi(user_time.substr(3, 2));
    int seconds      = stoi(user_time.substr(6, 2));
    int totalSeconds = hours * 3600 + minutes * 60 + seconds;

    // 根据秒数判断时间段
    if ((totalSeconds >= 7 * 3600 && totalSeconds <= 9 * 3600) ||
        (totalSeconds >= 18 * 3600 && totalSeconds <= 20 * 3600)) {
      commuteUsers.insert(user_id);
    } else if (totalSeconds >= 11 * 3600 && totalSeconds <= 13 * 3600) {
      lunchUsers.insert(user_id);
    } else if ((totalSeconds >= 22 * 3600 && totalSeconds <= 24 * 3600) ||
               (totalSeconds >= 0 && totalSeconds <= 1 * 3600)) {
      sleepUsers.insert(user_id);
    }
  }

  cout << commuteUsers.size() << " " << lunchUsers.size() << " "
       << sleepUsers.size() << endl;
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);

  solve();
  return 0;
}
```

