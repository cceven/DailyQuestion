# B. Two Large Bags

time limit per test: 1 second

memory limit per test: 256 megabytes

input: standard input

output: standard output

You have two large bags of numbers. Initially, the first bag contains $n$ numbers: $a_1, a_2, \ldots, a_n$, while the second bag is empty. You are allowed to perform the following operations:

-   Choose any number from the first bag and move it to the second bag.
-   Choose a number from the first bag that is also present in the second bag and increase it by one.

You can perform an unlimited number of operations of both types, in any order. Is it possible to make the contents of the first and second bags identical?

## **Input**

Each test contains multiple test cases. The first line contains the number of test cases $t$ ($1 \le t \le 10^4$). The description of the test cases follows.

The first line of each test case contains an integer $n$ ($2 \le n \le 1000$) — the length of the array $a$. It is guaranteed that $n$ is an even number.

The second line of each test case contains $n$ integers $a_1, a_2, \ldots, a_n$ ($1 \le a_i \le n$).

It is guaranteed that the sum of $n^2$ over all test cases does not exceed $10^6$.

## **Output**

For each test case, print "YES" if it is possible to equalize the contents of the bags. Otherwise, output "NO".

You can output each letter in any case (for example, "YES", "Yes", "yes", "yEs", "yEs" will be recognized as a positive answer).

## Example

### Input

```
9
2
1 1
2
2 1
4
1 1 4 4
4
3 4 3 3
4
2 3 4 4
6
3 3 4 5 3 3
6
2 2 2 4 4 4
8
1 1 1 1 1 1 1 4
10
9 9 9 10 10 10 10 10 10 10
```

### Output

```
Yes
No
Yes
Yes
No
Yes
No
Yes
Yes
```

### **Note**

Let's analyze the sixth test case: we will show the sequence of operations that leads to the equality of the bags. Initially, the first bag consists of the numbers $(3, 3, 4, 5, 3, 3)$, and the second bag is empty.

1.  In the first operation, move the number $3$ from the first bag to the second. State: $(3, 4, 5, 3, 3)$ and $(3)$.
2.  In the second operation, increase the number $3$ from the first bag by one. This operation is possible because the second bag contains the number $3$. State: $(4, 4, 5, 3, 3)$ and $(3)$.
3.  In the third operation, move the number $4$ from the first bag to the second. State: $(4, 5, 3, 3)$ and $(3, 4)$.
4.  In the fourth operation, increase the number $4$ from the first bag by one. State: $(5, 5, 3, 3)$ and $(3, 4)$.
5.  In the fifth operation, move the number $5$ from the first bag to the second. State: $(5, 3, 3)$ and $(3, 4, 5)$.
6.  In the sixth operation, increase the number $3$ from the first bag by one. State: $(5, 3, 4)$ and $(3, 4, 5)$.

As we can see, as a result of these operations, it is possible to make the contents of the bags equal, so the answer exists.

## 代码

​	首先记录所有数出现的次数到`cnt`中，然后用一个集合`set`存储不同的数。

​	遍历`set`，如果一个数出现的次数只有1次，那么`a`和`b`肯定不能相等，直接返回`No`。如果一个数出现了两次，那么这一数直接能达到相等，直接`continue`。如果一个数出现的次数大于两次，那么我们只取刚好能相等的两次，一次留给`a`，一次留给`b`，然后剩下的全部向上进行转换。

​	如果能够顺利遍历完，那么一定可以达成目的。

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  int n;
  cin >> n;
  set<int> a;                   // 存储不同的数
  unordered_map<int, int> cnt;  // 存储出现的次数
  for (int i = 0; i < n; i++) {
    int num;
    cin >> num;
    cnt[num]++;     // 次数增加
    a.insert(num);  // 存储有哪些数
  }
  // 开始从小到大进行遍历
  for (auto &num : a) {
    // 如果某个数只有一个，那么说明达不到要求，直接返回No
    if (cnt[num] == 1) {
      cout << "No" << endl;
      return;
    } else if (cnt[num] == 2) {
      // 如果某个数的次数为2，那么刚刚好可以进行分配，不用操作直接下一个
      continue;
    } else {
      // 如果个数大于2，那么留下1个给a，留下1个给b，其他的全部向上转换
      int remain_num = cnt[num] - 2;
      cnt[num] -= remain_num;
      a.insert(num + 1);  // 防止出现新数
      cnt[num + 1] += remain_num;
    }
  }
  // 如果能够遍历完，说明可以达到要求
  cout << "Yes" << endl;
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

