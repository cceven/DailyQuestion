# [**D - Bonfire**](https://atcoder.jp/contests/abc398/tasks/abc398_d)

![image-20250402002056797](https://gitee.com/chen-houchao/images/raw/master/202504020020099.png)

## 代码

​	这道题如果我们考虑烟雾的话，那么每次对每个烟雾进行移动是一个非常大的工作量，并且烟雾的数量也是非递减。所以我们考虑使用相对位置，移动火堆和人。

​	比如题目说到当字符为`N`时横坐标减，那么我们就当遍历到`N`时增加横坐标。记得每一次遍历的时候把当前火堆的位置加入烟雾位置，同时使用`set`进行坐标的存储，还可以防止烟雾位置的重复。

​	判断当前人的位置是否有烟雾我们直接使用`.find()`函数就可以了。

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  int N;
  pair<int, int> peo_pos, fire_pos;  // Takahashi的位置{R,C}，和火堆的位置
  string S;
  cin >> N >> peo_pos.first >> peo_pos.second >> S;
  fire_pos = { 0, 0 };           // 最开始火堆的位置
  set<pair<int, int>> smog_pos;  // 烟雾存在的位置
  smog_pos.insert(fire_pos);

  string ans;
  for (auto &c : S) {
    if (c == 'N') {
      peo_pos.first++;
      fire_pos.first++;
    } else if (c == 'S') {
      peo_pos.first--;
      fire_pos.first--;
    } else if (c == 'E') {
      peo_pos.second--;
      fire_pos.second--;
    } else if (c == 'W') {
      peo_pos.second++;
      fire_pos.second++;
    }

    smog_pos.insert(fire_pos);  // 每次火堆又产生了新的烟雾
    if (smog_pos.find(peo_pos) != smog_pos.end()) {
      ans += '1';
    } else {
      ans += '0';
    }
  }
  cout << ans;
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

