# B. Robot Program

time limit per test: 2 seconds

memory limit per test: 512 megabytes

input: standard input

output: standard output

There is a robot on the coordinate line. Initially, the robot is located at the point $x$ ($x \ne 0$). The robot has a sequence of commands of length $n$ consisting of characters, where L represents a move to the left by one unit (from point $p$ to point $(p-1)$) and R represents a move to the right by one unit (from point $p$ to point $(p+1)$).

The robot starts executing this sequence of commands (one command per second, in the order they are presented). However, whenever the robot reaches the point $0$, the counter of executed commands is reset (i. e. it starts executing the entire sequence of commands from the very beginning). If the robot has completed all commands and is not at $0$, it stops.

Your task is to calculate how many times the robot will enter the point $0$ during the next $k$ seconds.

## **Input**

The first line contains a single integer $t$ ($1 \le t \le 10^4$) — the number of test cases.

The first line of a test case contains three integers $n$, $x$ and $k$ ($1 \le n \le 2 \cdot 10^5$; $-n \le x \le n$; $n \le k \le 10^{18}$).

The second line of a test case contains a string $s$ consisting of $n$ characters L and/or R.

Additional constraint on the input: the sum of $n$ over all test cases doesn't exceed $2 \cdot 10^5$.

## **Output**

For each test case, print a single integer — the number of times the robot will enter the point $0$ during the next $k$ seconds.

## Example

### Input

```
6
3 2 6
LLR
2 -1 8
RL
4 -2 5
LRRR
5 3 7
LRRLL
1 1 1
L
3 -1 4846549234412827
RLR
```

### Output

```
1
4
1
0
1
2423274617206414
```

### Note

In the first example, the robot moves as follows: 2→1→0–→−1→−2→−12→1→0_→−1→−2→−1. The robot has completed all instructions from the sequence and is not at 00. So it stops after 55 seconds and the point 00 is entered once.

In the second example, the robot moves as follows: −1→0–→1→0–→1→0–→1→0–→1−1→0_→1→0_→1→0_→1→0_→1. The robot worked 88 seconds and the point 00 is entered 44 times.

In the third example, the robot moves as follows: −2→−3→−2→−1→0–→−1−2→−3→−2→−1→0_→−1. The robot worked 55 seconds and the point 00 is entered once.

In the fourth example, the robot moves as follows: 3→2→3→4→3→23→2→3→4→3→2. The robot has completed all instructions from the sequence and is not at 00. So it stops after 55 seconds, without reaching the point 00.

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;

void solve() {
  int n, x;
  ll k;
  cin >> n >> x >> k;
  string s;
  cin >> s;
  int curr_k = 1;  // 当前的时间
  int times  = 0;  // 次数
  // 第一次到0的时间，第二次到0的时间，循环周期
  int start_k = -1, second_k = -1, interval_k = -1;
  for (int i = 0; i < s.size() && curr_k <= k; i++) {
    // 先移动
    if (s[i] == 'L') {
      x--;
    } else {
      x++;
    }

    // 如果移动后到了0
    if (x == 0) {
      if (start_k == -1) {  // 标记第一次到达0
        start_k = curr_k;
      } else if (start_k != -1 && second_k == -1) {  // 标记第二次到达0
        second_k   = curr_k;
        interval_k = second_k - start_k;
        break;
      }

      times++;  // 次数增加
      i = -1;   // 重新开始移动
    }
    // 运行时间增加
    curr_k++;
  }
  // 如果时间范围内存在循环
  if (interval_k != -1)
    cout << 1 + (k - start_k) / interval_k << endl;
  else
    cout << times << endl;
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

- 先算出第一次到达0的时间，然后算出第二次到达0的时间（如果有，没有的话直接终止输出结果），那么之后一定会循环，直接用时间除以循环周期。
