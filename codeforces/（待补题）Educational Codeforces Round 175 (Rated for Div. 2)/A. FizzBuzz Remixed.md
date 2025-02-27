# A. FizzBuzz Remixed

time limit per test: 1 second

memory limit per test: 512 megabytes

input: standard input

output: standard output

FizzBuzz is one of the most well-known problems from coding interviews. In this problem, we will consider a remixed version of FizzBuzz:

Given an integer $n$, process all integers from $0$ to $n$. For every integer such that its remainders modulo $3$ and modulo $5$ are the same (so, for every integer $i$ such that $i \bmod 3 = i \bmod 5$), print FizzBuzz.

However, you don't have to solve it. Instead, given the integer $n$, you have to report how many times the correct solution to that problem will print FizzBuzz.

## **Input**

The first line contains one integer $t$ ($1 \le t \le 10^4$) — the number of test cases.

Each test case contains one line consisting of one integer $n$ ($0 \le n \le 10^9$).

## **Output**

For each test case, print one integer — the number of times the correct solution will print FizzBuzz with the given value of $n$.

## Example

### Input

```
7
0
5
15
42
1337
17101997
998244353
```

### Output

```
1
3
4
9
270
3420402
199648872
```

### Note

In the first test case, the solution will print FizzBuzz for the integer 00.

In the second test case, the solution will print FizzBuzz for the integers 0,1,20,1,2.

In the third test case, the solution will print FizzBuzz for the integers 0,1,2,150,1,2,15.

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;

void solve() {
  int n;
  cin >> n;
  int cycles    = n / 15;
  int remainder = n % 15;
  int sum       = cycles * 3 + min(remainder + 1, 3);
  cout << sum << endl;
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);

  int t;
  cin >> t;
  while (t--) solve();
  return 0;
}
```

- 如果`num%a=num%b`，那么`num=k*lcm(a,b)+r`，其中`r<min(a,b)`

![image-20250227225103811](https://gitee.com/chen-houchao/images/raw/master/img/20250227225103883.png)
