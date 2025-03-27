# B. Kevin and Geometry

time limit per test: 1 second

memory limit per test: 256 megabytes

input: standard input

output: standard output

Kevin has $n$ sticks with length $a_1,a_2,\ldots,a_n$.

Kevin wants to select $4$ sticks from these to form an isosceles trapezoid$^{\text{∗}}$ with a positive area. Note that rectangles and squares are also considered isosceles trapezoids. Help Kevin find a solution. If no solution exists, output $-1$.

$^{\text{∗}}$An [isosceles trapezoid](https://en.wikipedia.org/wiki/Isosceles_trapezoid) is a convex quadrilateral with a line of symmetry bisecting one pair of opposite sides. In any isosceles trapezoid, two opposite sides (the bases) are parallel, and the two other sides (the legs) are of equal length.

## **Input**

Each test contains multiple test cases. The first line contains the number of test cases $t$ ($1 \le t \le 10^4$). The description of the test cases follows.

The first line of each test case contains a single integer $n$ ($4 \le n \le 2\cdot 10^5$).

The second line contains $n$ integers $a_1, a_2, \ldots, a_n$ ($1 \le a_i \le 10^8$).

It is guaranteed that the sum of $n$ over all test cases does not exceed $2\cdot 10^5$.

## **Output**

For each test case, output $4$ integers — the lengths of sticks. If no solution exists, output $-1$.

If there are multiple solutions, print any of them.

## Example

### Input

```
7
4
5 5 5 10
4
10 5 10 5
4
1 2 3 4
4
1 1 1 3
6
4 2 1 5 7 1
6
10 200 30 300 30 100
4
100000000 100000000 1 2
```

### Output

```
5 5 5 10
5 5 10 10
-1
-1
1 1 4 5
-1
100000000 100000000 1 2
```

### **Note**

In the first test case, you can form an isosceles trapezoid with bases of length $5$ and $10$, and two legs of length $5$.

In the second test case, you can form an isosceles trapezoid with two bases of length $5$ and two legs of length $10$. A rectangle is considered an isosceles trapezoid here.

In the third test case, there are no sticks with the same length. It's impossible to form an isosceles trapezoid.

In the fourth test case, it's impossible to form an isosceles trapezoid with a positive area.

## 代码

​	每次读取一个数，并判断是否已经有相同的数，并且现在的数量<=1（防止多个重复的数），如果有的话就放进重复数集合里面，同时从原来的集合中去除掉这个数。

​	数据读取完之后，判断重复的数是否>=2，如果是的话那么可以组成矩形，直接输出。如果重复的数==0的话，那么说明无解。

​	接下来就是只有一组重复的数的情况，我们直接寻找最小的差，最后腰长c是否满足`2*c>abs(a-b)`

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;

void solve() {
  int n;
  cin >> n;
  multiset<int> a;  // 存储没有相同数的数
  set<int> same_a;  // 存在相同数的集合

  for (int i = 0; i < n; i++) {
    int num;
    cin >> num;
    // 如果说已经有了num，并且之前没有相同的
    if (a.count(num) && same_a.count(num) == 0) {
      same_a.insert(num);
      a.erase(num);
      continue;
    }

    a.insert(num);
  }
  // 如果说有两对相同的数，直接输出结果
  if (same_a.size() >= 2) {
    cout << *same_a.begin() << ' ' << *same_a.begin() << ' ' << *same_a.rbegin()
         << ' ' << *same_a.rbegin() << endl;
    return;
  } else if (same_a.size() == 0)  // 如果说没有相同的数，那么无解
  {
    cout << "-1" << endl;
    return;
  }

  // 有一对相同的数
  vector<int> nums(a.begin(), a.end());
  sort(nums.begin(), nums.end());
  int min_diff = INT_MAX;  // 最小的差
  int num1, num2;          // 最小的差的两个数
  for (int i = 0; i < nums.size() - 1; i++) {
    // 更新最小差
    if (abs(nums[i] - nums[i + 1]) < min_diff) {
      min_diff = abs(nums[i] - nums[i + 1]);
      num1     = nums[i];
      num2     = nums[i + 1];
    }
  }
  // 唯一的一个有相同数的数
  int same_num = *same_a.begin();
  // 如果符合等腰梯形的条件
  if (same_num * 2 > min_diff) {
    cout << num1 << " " << num2 << " " << same_num << " " << same_num << endl;
  } else {  // 不符合等腰梯形的条件
    cout << "-1" << endl;
  }
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

