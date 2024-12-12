## **F - Double Sum**

https://atcoder.jp/contests/abc351/tasks/abc351_f

### 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;
struct aNum {
    ll value;   // 相应的值
    ll oriPos;  // 原始的位置
};
ll lowbit(const ll &n) {
  return n & (-n);
}
// 树状数组：求前x项和
ll getSum(const vector<ll> &BIT, ll x) {
  ll result = 0;
  while (x) {
    result += BIT[x];
    x -= lowbit(x);
  }
  return result;
}
// 树状数组：某一位加上数字
void updateBIT(vector<ll> &BIT, ll index, ll value) {
  while (index < BIT.size()) {
    BIT[index] += value;
    index += lowbit(index);
  }
}

void solve() {
  ll N;
  cin >> N;
  vector<aNum> A(N + 1);
  for (ll i = 1; i <= N; i++) {
    cin >> A[i].value;
    A[i].oriPos = i;
  }
  // 按照大小排序
  sort(A.begin() + 1, A.end(), [](const aNum &a, const aNum &b) {
    if (a.value == b.value) return a.oriPos < b.oriPos;
    return a.value < b.value;
  });
  vector<ll> sizePos(N + 1);  // 存储大小的位置
  for (ll i = 1; i <= N; i++) {
    sizePos[A[i].oriPos] = i;
  }
  // 复原
  sort(A.begin() + 1, A.end(),
       [](const aNum &a, const aNum &b) { return a.oriPos < b.oriPos; });
  // id在当前数字前面，且小于当前数字的数字个数（按照数字大小排的序）
  vector<ll> ifAppear(N + 1);
  // id在当前数字前面，且小于当前数字的和（按照数字大小排的序）
  vector<ll> sum(N + 1);
  ll result = 0;  // 结果
  for (ll i = 1; i <= N; i++) {
    // 加上x个当前数字，x为小于当前数，且在当前数字前面的数字的数字个数
    result += A[i].value * getSum(ifAppear, sizePos[i] - 1);
    // 减去小于当前的数，且在当前数字前面的数字和
    result -= getSum(sum, sizePos[i] - 1);
    // 当数字已经被操作过后，ifAppear+=1，说明originPos小于后面操作的数字
    updateBIT(ifAppear, sizePos[i], 1);
    // 当数字已经被操作过后，sum加上当前的值，使得后面操作的数字可以减去
    updateBIT(sum, sizePos[i], A[i].value);
  }
  cout << result;
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);

  solve();
  return 0;
}

```

- 题目相当于求每一个数字与前面小于自己的数字的差的和

- 使用了`sum`存储小于当前的数，且在原数组中在当前数字前面的数字和

- 使用了`ifAppear`存储了小于当前数，且在原数组中在当前数字前面的数字的数字个数

- 核心代码

  ```cpp
    for (ll i = 1; i <= N; i++) {
      // 加上x个当前数字，x为小于当前数，且在当前数字前面的数字的数字个数
      result += A[i].value * getSum(ifAppear, sizePos[i] - 1);
      // 减去小于当前的数，且在当前数字前面的数字和
      result -= getSum(sum, sizePos[i] - 1);
      // 当数字已经被操作过后，ifAppear+=1，说明originPos小于后面操作的数字
      updateBIT(ifAppear, sizePos[i], 1);
      // 当数字已经被操作过后，sum加上当前的值，使得后面操作的数字可以减去
      updateBIT(sum, sizePos[i], A[i].value);
    }
  ```

  