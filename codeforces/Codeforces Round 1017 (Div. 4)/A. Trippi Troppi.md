# A. Trippi Troppi

time limit per test: 1 second

memory limit per test: 256 megabytes

input: standard input

output: standard output

Trippi Troppi resides in a strange world. The ancient name of each country consists of three strings. The first letter of each string is concatenated to form the country's modern name.

Given the country's ancient name, please output the modern name.

## **Input**

The first line contains an integer $t$ – the number of independent test cases ($1 \leq t \leq 100$).

The following $t$ lines each contain three space-separated strings. Each string has a length of no more than $10$, and contains only lowercase Latin characters.

## **Output**

For each test case, output the string formed by concatenating the first letter of each word.

## Example

### Input

```
7
united states america
oh my god
i cant lie
binary indexed tree
believe in yourself
skibidi slay sigma
god bless america
```

### Output

```
usa
omg
icl
bit
biy
sss
gba
```

## 代码

```cpp
#include <bits/stdc++.h>
using namespace std;

void solve() {
  string a, b, c;
  cin >> a >> b >> c;
  string ans = a.substr(0, 1) + b.substr(0, 1) + c.substr(0, 1);
  cout << ans << endl;
}

int main() {
  int t = 1;
  cin >> t;
  while (t--) {
    solve();
  }
  return 0;
}
```

### 使用索引访问string的问题

​	如果使用索引访问`string`的元素，比如`s[0]`，那么返回的值是`char`类型，不能直接用于字符串的拼接。

​	如果需要进行字符串的拼接，并且使用的是字符串的单个元素，可以使用`substr()`函数。

![image-20250414113559237](https://gitee.com/chen-houchao/images/raw/master/202504141138023.png)

