# B. Substring and Subsequence

time limit per test: 2 seconds

memory limit per test: 256 megabytes

input: standard input

output: standard output

You are given two strings $a$ and $b$, both consisting of lowercase Latin letters.

A subsequence of a string is a string which can be obtained by removing several (possibly zero) characters from the original string. A substring of a string is a contiguous subsequence of that string.

For example, consider the string abac:

-   a, b, c, ab, aa, ac, ba, bc, aba, abc, aac, bac and abac are its subsequences;
-   a, b, c, ab, ba, ac, aba, bac and abac are its substrings.

Your task is to calculate the minimum possible length of the string that contains $a$ as a substring and $b$ as a subsequence.

## **Input**

The first line contains a single integer $t$ ($1 \le t \le 10^3$) — the number of test cases.

The first line of each test case contains a string $a$ ($1 \le |a| \le 100$), consisting of lowercase Latin letters.

The second line of each test case contains a string $b$ ($1 \le |b| \le 100$), consisting of lowercase Latin letters.

## **Output**

For each test case, print a single integer — the minimum possible length of the string that contains $a$ as a substring and $b$ as a subsequence.

## Example

### Input

```
5
aba
cb
er
cf
mmm
mmm
contest
test
cde
abcefg
```

### Output

```
4
4
3
7
7
```

### **Note**

In the examples below, the characters that correspond to the subsequence equal to $b$ are bolded.

In the first example, one of the possible answers is **c**a**b**a.

In the second example, one of the possible answers is er**cf**.

In the third example, one of the possible answers is **mmm**.

In the fourth example, one of the possible answers is con**test**.

In the fifth example, one of the possible answers is **abc**d**efg**.

## 代码

**暴力**、**贪心**

从字符串`b`的每一个索引（`i`）开始，以`j`为匹配末尾，寻找能够匹配的最大长度（即`j - i`），当前索引寻找完后更新答案（`n + m - (j - i )`）。

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  string a, b;
  cin >> a >> b;
  int n = a.size(), m = b.size();
  int ans = n + m;  // 最坏的情况，
  for (int i = 0; i < m; i++) {
    int j = i;  // 从i开始找匹配的，j为匹配的字符串末端
    // 遍历字符串a，寻找匹配的
    for (auto &c : a) {
      // 如果匹配上了，那么j++
      if (c == b[j]) j++;
      // 如果已经匹配完了，那么直接break
      if (j == m) break;
    }

    // 更新最小答案，(j-i)是当前匹配的长度
    ans = min(ans, n + m - (j - i));
  }
  cout << ans << endl;
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

