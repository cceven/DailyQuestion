# [[ABC388E] Simultaneous Kagamimochi](https://atcoder.jp/contests/abc388/tasks/abc388_e)

## 题面翻译

### 题目描述

有 $N$ 个大小不一的饼。第 $i$ 个饼的大小为 $a_i$（$1 \le i \le N$）。

对于任意两个大小分别为 $a$ 和 $b$ 的饼 $A$ 和 $B$，如果 $a$ 小于或等于 $b$ 的一半，即 $a\le \frac{b}{2}$，则可以将饼 $A$ 放在饼 $B$ 上制作一个“镜饼”。

从 $N$ 个饼中任选两个，使得其中一个饼放在另一个饼上制作一个“镜饼”。

需要求出可以**同时**制作多少种不同的“镜饼”。

**Translate by [chinazhanghaoxun](https://luogu.com.cn/user/684848)。**

### 输入格式

输入将以以下格式通过标准输入给出：

> $N \ A_1\ A_2\ \dots\ A_N$

### 输出格式

输出可以制作的镜饼数。
### 数据限制
- $2\le N\le 5\times 10^5$
- $1\le A_i \le 10^9(1\le i\le N)$
- $A_i\le A_{i+1}(1\le i\le N)$
- 输入值均为整数

## 题目描述

[problemUrl]: https://atcoder.jp/contests/abc388/tasks/abc388_e

$ N $ 個の餅が小さいほうから順に並んでいます。 $ i $ 番目 $ (1\leq\ i\leq\ N) $ の餅の大きさは $ A\ _\ i $ です。

$ 2 $ つの餅 $ A,B $ の大きさをそれぞれ $ a,b $ としたとき、$ a $ が $ b $ の半分以下であるとき、かつそのときに限り、餅 $ A $ を餅 $ B $ の上に乗せて鏡餅を $ 1 $ つ作ることができます。

同時にいくつの鏡餅を作ることができるか求めてください。

より厳密には、以下ができるような最大の非負整数 $ K $ を求めてください。

- $ N $ 個の餅から $ 2K $ 個の餅を選んで $ K $ 個の $ 2 $ つ組に分け、それぞれの組について一方をもう一方の上に乗せることで鏡餅を $ K $ 個作る。

## 输入格式

入力は以下の形式で標準入力から与えられる。

> $ N $ $ A\ _\ 1 $ $ A\ _\ 2 $ $ \dotsc $ $ A\ _\ N $

## 输出格式

同時に $ K $ 個鏡餅を作れるような最大の $ K $ を出力せよ。

## 样例 #1

### 样例输入 #1

```
6
2 3 4 4 7 10
```

### 样例输出 #1

```
3
```

## 样例 #2

### 样例输入 #2

```
3
387 388 389
```

### 样例输出 #2

```
0
```

## 样例 #3

### 样例输入 #3

```
24
307 321 330 339 349 392 422 430 477 481 488 537 541 571 575 602 614 660 669 678 712 723 785 792
```

### 样例输出 #3

```
6
```

## 提示

### 制約

- $ 2\leq\ N\leq\ 5\times\ 10\ ^\ 5 $
- $ 1\leq\ A\ _\ i\leq\ 10\ ^\ 9\ (1\leq\ i\leq\ N) $
- $ A\ _\ i\leq\ A\ _\ {i+1}\ (1\leq\ i\lt\ N) $
- 入力はすべて整数

### Sample Explanation 1

与えられた餅の大きさは以下のようになっています。 !\[\](https://img.atcoder.jp/abc388/29024766d11c2d88b06c92b2081129f5.png) このとき、以下の $ 3 $ つの鏡餅を同時に作ることができます。 !\[\](https://img.atcoder.jp/abc388/26686710916fe3623058f6000669e049.png) $ 6 $ つの餅から $ 4 $ つ以上の鏡餅を作ることはできないので、`3` を出力してください。

### Sample Explanation 2

鏡餅を $ 1 $ つも作ることができない場合もあります。

## 代码

### 原代码（测试点通过，提交不通过）

![image-20250117015443146](https://gitee.com/chen-houchao/images/raw/master/img/20250117015443217.png)

```cpp
#include <bits/stdc++.h>
using namespace std;
#define endl "\n"

void solve() {
  long long N;
  cin >> N;
  long long sum = 0;
  vector<long long> mochis(N);
  for (long long i = 0; i < N; i++) {
    cin >> mochis[i];
  }  // 输入年糕大小
  sort(mochis.begin(), mochis.end(),
       [](long long a, long long b) { return a < b; });  // 从小到大排序
  for (long long i = 0; i < N; i++) {
    auto left = lower_bound(mochis.begin(), mochis.end(), mochis[i] * 2);
    // 找到了
    if (left != mochis.end()) {
      mochis.erase(left);
      sum += 1;
    }
  }
  cout << sum << endl;
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);

  solve();
  return 0;
}
```

### 优化后的代码

```cpp
#include <bits/stdc++.h>
using namespace std;
#define endl "\n"

void solve() {
  long long N;
  cin >> N;
  long long sum = 0;
  vector<long long> mochis(N);
  for (long long i = 0; i < N; i++) {
    cin >> mochis[i];
  }  // 输入年糕大小
  sort(mochis.begin(), mochis.end());  // 从小到大排序
  int left = 0, right = N / 2;
  while (left < N && right < N) {
    if (mochis[left] * 2 <= mochis[right]) {
      sum++;
      left++;
      right++;
    } else {
      right++;
    }
  }
  cout << sum << endl;
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);

  solve();
  return 0;
}
```

- 使用双指针，`left`从0开始，`right`从`N/2`开始，此时为最终`sum`最大的情况，即所有一对一匹配。