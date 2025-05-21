# C. Breach of Faith

time limit per test: 2 seconds

memory limit per test: 256 megabytes

input: standard input

output: standard output

You and your team have worked tirelessly until you have a sequence $a_1, a_2, \ldots, a_{2n+1}$ of positive integers satisfying these properties.

-   $1 \le a_i \le 10^{18}$ for all $1 \le i \le 2n + 1$.
-   $a_1, a_2, \ldots, a_{2n+1}$ are pairwise **distinct**.
-   $a_1 = a_2 - a_3 + a_4 - a_5 + \ldots + a_{2n} - a_{2n+1}$.

However, the people you worked with sabotaged you because they wanted to publish this sequence first. They deleted one number from this sequence and shuffled the rest, leaving you with a sequence $b_1, b_2, \ldots, b_{2n}$. You have forgotten the sequence $a$ and want to find a way to recover it.

If there are many possible sequences, you can output any of them. It can be proven under the constraints of the problem that at least one sequence $a$ exists.

## **Input**

Each test contains multiple test cases. The first line contains the number of test cases $t$ ($1 \le t \le 10^4$). The description of the test cases follows.

The first line of each test case contains one integer $n$ ($1 \leq n \leq 2 \cdot 10^5$).

The second line of each test case contains $2n$ **distinct** integers $b_1, b_2, \ldots, b_{2n}$ ($1 \leq b_i \leq 10^9$), denoting the sequence $b$.

It is guaranteed that the sum of $n$ over all test cases does not exceed $2 \cdot 10^5$.

## **Output**

For each test case, output $2n+1$ **distinct** integers, denoting the sequence $a$ ($1 \leq a_i \leq 10^{18}$).

If there are multiple possible sequences, you can output any of them. The sequence $a$ should satisfy the given conditions, and it should be possible to obtain $b$ after deleting one element from $a$ and shuffling the remaining elements.

## Example

### Input

```
4
1
9 2
2
8 6 1 4
3
99 2 86 33 14 77
2
1 6 3 2
```

### Output

```
7 9 2
1 8 4 6 9
86 99 2 77 69 14 33
4 6 1 2 3
```

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;

void solve() {
  int n;
  cin >> n;  // 2n个数字
  vector<int> b(2 * n);
  for (int i = 0; i < 2 * n; i++) {
    cin >> b[i];
  }
  // 从大到小进行排序
  sort(b.begin(), b.end(), greater<int>());
  // 计算相邻项的差值之和
  int tot = 0;
  for (int i = 0; i < 2 * n - 1; i += 2) {
    tot += b[i] - b[i + 1];
  }
  // 原来的a2变为a1，构造新的a2
  ll new_a2 = 2 * b[0] - tot;
  // 新构造的a2一定与之前所有的数字不同且最大，可以证明。直接输出结果
  cout << b[0] << " " << new_a2;
  for (int i = 1; i < 2 * n; i++) {
    cout << " " << b[i];
  }
  cout << endl;
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);
  int t = 1;
  cin >> t;
  while (t--) solve();
  return 0;
}
```

- 相邻差值之和`tot`可以看过一个一个的区间之和相加，所以最大也到不了整个大区间的最大值（也就是原来的`a2`现在的`a1`），就可以保证新构造的`a2(2*a2（原来的）-tot)`与原来的所有数字不重复

- 如果要进行从大到小的排序的话`sort()`函数可以直接使用`greater<int>()`