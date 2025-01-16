# [[ABC388C] Various Kagamimochi](https://atcoder.jp/contests/abc388/tasks/abc388_c)

## 题面翻译

### 题目描述

有 $N$ 个大小不一的饼。第 $i$ 个饼的大小为 $a_i$（$1 \le i \le N$）。

对于任意两个大小分别为 $a$ 和 $b$ 的饼 $A$ 和 $B$，如果 $a$ 小于或等于 $b$ 的一半，即 $a\le \frac{b}{2}$，则可以将饼 $A$ 放在饼 $B$ 上制作一个“镜饼”。

从 $N$ 个饼中任选两个，使得其中一个饼放在另一个饼上制作一个“镜饼”。

需要求出可以制作多少种不同的“镜饼”。

此外，即使构成镜饼的饼的大小相同，只要至少有一个是不同的饼，就可以算作是另一种类型的镜饼。

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

[problemUrl]: https://atcoder.jp/contests/abc388/tasks/abc388_c

$ N $ 個の餅が小さいほうから順に並んでいます。 $ i $ 番目 $ (1\leq\ i\leq\ N) $ の餅の大きさは $ A\ _\ i $ です。

$ 2 $ つの餅 $ A,B $ の大きさをそれぞれ $ a,b $ としたとき、$ a $ が $ b $ の半分以下であるとき、かつそのときに限り、餅 $ A $ を餅 $ B $ の上に乗せて鏡餅を $ 1 $ つ作ることができます。

$ N $ 個の餅から $ 2 $ つの餅を選び、一方をもう一方の上に乗せることで鏡餅を $ 1 $ つ作ります。

何種類の鏡餅を作ることができるか求めてください。

ただし、鏡餅を構成する餅の大きさが同じでも、少なくとも一方が異なる餅であれば別の種類の鏡餅として数えます。

## 输入格式

入力は以下の形式で標準入力から与えられる。

> $ N $ $ A\ _\ 1 $ $ A\ _\ 2 $ $ \cdots $ $ A\ _\ N $

## 输出格式

作ることができる鏡餅の種類数を出力せよ。

## 样例 #1

### 样例输入 #1

```
6
2 3 4 4 7 10
```

### 样例输出 #1

```
8
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
32
1 2 4 5 8 10 12 16 19 25 33 40 50 64 87 101 149 175 202 211 278 314 355 405 412 420 442 481 512 582 600 641
```

### 样例输出 #3

```
388
```

## 提示

### 制約

- $ 2\leq\ N\leq\ 5\times\ 10\ ^\ 5 $
- $ 1\leq\ A\ _\ i\leq\ 10\ ^\ 9\ (1\leq\ i\leq\ N) $
- $ A\ _\ i\leq\ A\ _\ {i+1}\ (1\leq\ i\lt\ N) $
- 入力はすべて整数

### Sample Explanation 1

与えられた餅の大きさは以下のようになっています。 !\[\](https://img.atcoder.jp/abc388/29024766d11c2d88b06c92b2081129f5.png) このとき、以下の $ 8 $ 種類の鏡餅を作ることができます。 !\[\](https://img.atcoder.jp/abc388/0b69fbe457f2c4298173acce2faab37e.png) 大きさ $ 4 $ の餅の上に大きさ $ 2 $ の餅を乗せた鏡餅や、大きさ $ 10 $ の餅の上に大きさ $ 4 $ の餅を乗せた鏡餅は $ 2 $ 種類あることに注意してください。

### Sample Explanation 2

鏡餅を $ 1 $ 種類も作ることができない場合もあります。

## 代码

### 原代码

![image-20250117014035482](https://gitee.com/chen-houchao/images/raw/master/img/20250117014035522.png)

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
       [](long long a, long long b) { return a < b; });  // 把年糕从小到大排序
  for (long long i = 0; i < N; i++) {
    // 而分叉找到第一个符合条件的年糕
    long long left = lower_bound(mochis.begin(), mochis.end(), mochis[i] * 2) -
                     mochis.begin();
    long long right = N;
    // 符合条件的年糕的数量
    sum += right - left;
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

![image-20250117014018043](https://gitee.com/chen-houchao/images/raw/master/img/20250117014023112.png)

```cpp
#include <bits/stdc++.h>
using namespace std;
#define endl "\n"

void solve() {
  long long N;
  cin >> N;
  vector<long long> mochis(N);

  for (long long i = 0; i < N; i++) {
    cin >> mochis[i];
  }

  // 从小到大排序，sort默认就是从小到大排序所以不用使用lambda
  sort(mochis.begin(), mochis.end());

  long long sum   = 0;
  long long right = 0;  // 使用双指针，右指针初始化

  // 双指针优化
  for (long long i = 0; i < N; i++) {
    // 移动右指针找到 mochis[i] * 2 位置
    while (right < N && mochis[right] < mochis[i] * 2) {
      ++right;
    }
    // 计算符合条件的数量
    sum += N - right;
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

- `sort`默认就是从小到大排序，所以不用使用lambda表达式
- 使用双指针替代二分查找`lower_bound()`