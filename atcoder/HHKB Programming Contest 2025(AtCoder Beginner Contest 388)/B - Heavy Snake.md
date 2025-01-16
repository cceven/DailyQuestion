# [[ABC388B] Heavy Snake](https://atcoder.jp/contests/abc388/tasks/abc388_b)

## 题面翻译

### 题目描述
有 $N$ 条蛇。

起初，第 $i$ 条蛇，$T_i$ 粗， $L_i$ 长。

蛇的重量是其厚度和长度的乘积。

对于满足 $1 \leq k \leq D$ 的每个整数 $k$ ，求当所有蛇的长度都增长 $k$ 时，最重的蛇的重量。

### 输入
输入通过标准输入，格式如下。

>$N$ $D$  
>$T_1$ $L_1$  
>$T_2$ $L_2$  
>$\vdots$  
>$T_N$ $L_N$

- $1 \leq N, D \leq 100$
- $1 \leq T_i, L_i \leq 100$

### 输出
输出 $D$ 行。第 $k$ 行输出当所有蛇的长度增长 $k$ 时，最重蛇的重量。

uid:1277793

## 题目描述

[problemUrl]: https://atcoder.jp/contests/abc388/tasks/abc388_b

$ N $ 匹のヘビがいます。

はじめ、$ i $ 匹目のヘビの太さは $ T_i $、長さは $ L_i $ です。

ヘビの重さは太さと長さの積となります。

$ 1\ \leq\ k\ \leq\ D $ を満たす各整数 $ k $ について、すべてのヘビの長さが $ k $ 伸びたときの最も重いヘビの重さを求めてください。

## 输入格式

入力は以下の形式で標準入力から与えられる。

> $ N $ $ D $ $ T_1 $ $ L_1 $ $ T_2 $ $ L_2 $ $ \vdots $ $ T_N $ $ L_N $

## 输出格式

$ D $ 行出力せよ。$ k $ 行目には、すべてのヘビの長さが $ k $ 伸びたときの最も重いヘビの重さを出力せよ。

## 样例 #1

### 样例输入 #1

```
4 3
3 3
5 1
2 4
1 10
```

### 样例输出 #1

```
12
15
20
```

## 样例 #2

### 样例输入 #2

```
1 4
100 100
```

### 样例输出 #2

```
10100
10200
10300
10400
```

## 提示

### 制約

- $ 1\ \leq\ N,\ D\ \leq\ 100 $
- $ 1\ \leq\ T_i,\ L_i\ \leq\ 100 $
- 入力される値はすべて整数

### Sample Explanation 1

すべてのヘビの長さが $ 1 $ 伸びたとき、ヘビの重さはそれぞれ $ 12,\ 10,\ 10,\ 11 $ となるので $ 1 $ 行目には $ 12 $ を出力します。 すべてのヘビの長さが $ 2 $ 伸びたとき、ヘビの重さはそれぞれ $ 15,\ 15,\ 12,\ 12 $ となるので $ 2 $ 行目には $ 15 $ を出力します。 すべてのヘビの長さが $ 3 $ 伸びたとき、ヘビの重さはそれぞれ $ 18,\ 20,\ 14,\ 13 $ となるので $ 3 $ 行目には $ 20 $ を出力します。

## 代码

### 原代码

```cpp
#include <bits/stdc++.h>
using namespace std;
#define endl "\n"

struct snack {
    int T, L;
    int weight;
};

void solve() {
  int N, D;
  cin >> N >> D;
  vector<snack> snacks(N);  // N条蛇
  for (int i = 0; i < N; i++) {
    cin >> snacks[i].T >> snacks[i].L;
    snacks[i].weight = snacks[i].T * snacks[i].L;
  }
  for (int i = 1; i <= D; i++) {
    for (int j = 0; j < N; j++) {  // 更新每条蛇的体重
      snacks[j].weight += snacks[j].T;
    }
    // 按照体重进行排序
    sort(snacks.begin(), snacks.end(),
         [](snack a, snack b) { return a.weight > b.weight; });
    cout << snacks[0].weight << endl;
  }
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);

  solve();
  return 0;
}
```

