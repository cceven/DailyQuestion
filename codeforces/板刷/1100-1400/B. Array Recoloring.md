# B. Array Recoloring

time limit per test: 2 seconds

memory limit per test: 256 megabytes

input: standard input

output: standard output

You are given an integer array $a$ of size $n$. Initially, all elements of the array are colored red.

You have to choose exactly $k$ elements of the array and paint them blue. Then, while there is at least one red element, you have to select any red element with a blue neighbor and make it blue.

The cost of painting the array is defined as the sum of the first $k$ chosen elements and the last painted element.

Your task is to calculate the maximum possible cost of painting for the given array.

## **Input**

The first line contains a single integer $t$ ($1 \le t \le 10^3$) — the number of test cases.

The first line of each test case contains two integers $n$ and $k$ ($2 \le n \le 5000$; $1 \le k \lt n$).

The second line contains $n$ integers $a_1, a_2, \dots, a_n$ ($1 \le a_i \le 10^9$).

Additional constraint on the input: the sum of $n$ over all test cases doesn't exceed $5000$.

## **Output**

For each test case, print a single integer — the maximum possible cost of painting for the given array.

## Example

### Input

```
3
3 1
1 2 3
5 2
4 2 3 1 3
4 3
2 2 2 2
```

### Output

```
5
10
8
```

### **Note**

In the first example, you can initially color the $2$\-nd element, and then color the elements in the order $1, 3$. Then the cost of painting is equal to $2+3=5$.

In the second example, you can initially color the elements $1$ and $5$, and then color the elements in the order $2, 4, 3$. Then the cost of painting is equal to $4+3+3=10$.

In the third example, you can initially color the elements $2, 3, 4$, and then color the $1$\-st element. Then the cost of painting is equal to $2+2+2+2=8$.

## 代码

​	如果`k >= 2`，那么说明一定可以选择到最大的`k`个数，因为每次我们可以自己选择染色。如果`k == 1`，那么最后的结果一定包含第一个数或者最后一个数，使用`max`函数进行选择即可。

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  int n, k;
  cin >> n >> k;
  vector<int> a(n);
  for (auto &num : a) cin >> num;
  ll ans = 0;
  if (k > 1) {
    // 如果k>1,那么说明一定可以得到最大的k个数
    sort(a.begin(), a.end(), greater<int>());
    ans = reduce(a.begin(), a.begin() + k + 1, 0LL);
  } else {
    // 如果k==1,那么最后一个数要么为第一个数要么为最后一个数
    int l = *max_element(a.begin(), a.end() - 1);
    int r = *max_element(a.begin() + 1, a.end());
    ans   = max(a[0] + r, l + a.back());
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

