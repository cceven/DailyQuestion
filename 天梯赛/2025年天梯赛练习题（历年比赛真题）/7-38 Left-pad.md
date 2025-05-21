# **7-38 Left-pad**

分数 20

作者 陈越

单位 浙江大学

根据新浪微博上的消息，有一位开发者不满NPM（Node Package Manager）的做法，收回了自己的开源代码，其中包括一个叫left-pad的模块，就是这个模块把javascript里面的React/Babel干瘫痪了。这是个什么样的模块？就是在字符串前填充一些东西到一定的长度。例如用`*`去填充字符串`GPLT`，使之长度为10，调用left-pad的结果就应该是`******GPLT`。Node社区曾经对left-pad紧急发布了一个替代，被严重吐槽。下面就请你来实现一下这个模块。

## 输入格式：

输入在第一行给出一个正整数`N`（≤104）和一个字符，分别是填充结果字符串的长度和用于填充的字符，中间以1个空格分开。第二行给出原始的非空字符串，以回车结束。

## 输出格式：

在一行中输出结果字符串。

## 输入样例1：

```in
15 _
I love GPLT
```

## 输出样例1：

```out
____I love GPLT
```

## 输入样例2：

```
4 *
this is a sample for cut
```

## 输出样例2：

```
 cut
```

代码长度限制

16 KB

时间限制

250 ms

内存限制

64 MB

栈限制

8192 KB

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;

void solve() {
  int N;
  char c;
  cin >> N >> c;
  cin.ignore();
  string s;
  getline(cin, s);

  // 判断输出
  if (s.size() > N)
    cout << s.substr(s.size() - N, N) << endl;
  else
    cout << setfill(c) << setw(N) << s << endl;
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);

  solve();
  return 0;
}
```

