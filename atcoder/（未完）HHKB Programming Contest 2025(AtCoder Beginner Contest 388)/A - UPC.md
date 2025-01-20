# [[ABC388A] ?UPC](https://atcoder.jp/contests/abc388/tasks/abc388_a)

## 题面翻译

给你一串字母，输出它的第一个字母加上 `UPC`。

## 题目描述

[problemUrl]: https://atcoder.jp/contests/abc388/tasks/abc388_a

文字列 $ S $ が与えられます。ここで、$ S $ の $ 1 $ 文字目は英大文字、$ 2 $ 文字目以降は英小文字です。

$ S $ の $ 1 $ 文字目と `UPC` をこの順に結合した文字列を出力してください。

## 输入格式

入力は以下の形式で標準入力から与えられる。

> $ S $

## 输出格式

$ S $ の $ 1 $ 文字目と `UPC` をこの順に結合した文字列を出力せよ。

## 样例 #1

### 样例输入 #1

```
Kyoto
```

### 样例输出 #1

```
KUPC
```

## 样例 #2

### 样例输入 #2

```
Tohoku
```

### 样例输出 #2

```
TUPC
```

## 提示

### 制約

- $ S $ は長さ $ 1 $ 以上 $ 100 $ 以下の文字列
- $ S $ の $ 1 $ 文字目は英大文字
- $ S $ の $ 2 $ 文字目以降は英小文字

### Sample Explanation 1

`Kyoto` の $ 1 $ 文字目は `K` であるため、`K` と `UPC` を結合した `KUPC` を出力します。

## 代码

```cpp
#include <bits/stdc++.h>
using namespace std;
#define endl "\n"
void solve() {
  string S;
  cin >> S;
  cout << S[0] << "UPC";
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);

  solve();
  return 0;
}
```

