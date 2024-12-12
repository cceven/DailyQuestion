# Test of Love

https://codeforces.com/contest/1992/problem/D

## 题面翻译

ErnKor 愿意为 Julen 做任何事情，甚至愿意游过鳄鱼出没的沼泽。我们决定测试一下这份爱。ErnKor 必须游过一条宽 $1$ 米、长 $n$ 米的河流。

这条河水非常冷。因此，**总共**（即从 $0$ 到 $n+1$ 的整个游泳过程中）ErnKor 最多只能在水中游 $k$ 米。为了人类的利益，我们不仅向河里添加了鳄鱼，还添加了他可以跳上去的原木。我们的测试如下：

最初，ErnKor 在左岸，需要到达右岸。它们分别位于 $0$ 和 $n+1$ 米处。河流可以表示为 $n$ 个河段，每个河段的长度为 $1$ 米。每个河段要么包含一根原木“L”，要么包含一条鳄鱼“C”，要么只包含一条水“W”。ErnKor 可以按以下方式移动：

- 如果他在水面上（即在河岸上或在原木上），他最多可以向前跳跃 $m$ ( $1 \le m \le 10$ ) 米（他可以跳上河岸、原木或跳入水中）。
- 如果他在水中，他只能游到下一个河段（或者如果他在第 $n$ 米处，则游到河岸）。
- ErnKor 无论如何都不能降落在有鳄鱼的河段上。

确定 ErnKor 是否可以到达右岸。

### **输入**

第一行包含一个整数 $t$ ( $1 \le t \le 10^4$ ) — 测试用例的数量。

每个测试用例的第一行包含三个数字 $n, m, k$ ( $0 \le k \le 2 \cdot 10^5$ , $1 \le n \le 2 \cdot 10^5$ , $1 \le m \le 10$ ) — 河流的长度、ErnKor 可以跳跃的距离以及 ErnKor 可以不冻僵地游动的米数。

每个测试用例的第二行包含一个长度为 $n$ 的字符串 $a$ 。 $a_i$ 表示位于第 $i$ 米处的对象。 ( $a_i \in \{$ 'W','C','L' $\}$ )

保证所有测试用例的 $n$ 之和不超过 $2 \cdot 10^5$ 。

### **输出**

对于每个测试案例，如果 ErnKor 可以通过测试，则输出“YES”，否则输出“NO”。

您可以以任何大小写（大写或小写）输出答案。例如，字符串“yEs”、“yes”、“Yes”和“YES”将被识别为肯定响应。

### Example

#### Input

```
6
6 2 0
LWLLLW
6 1 1
LWLLLL
6 1 1
LWLLWL
6 2 15
LWLLCC
6 10 0
CCCCCC
6 6 1
WCCCCW
```

#### Output

```
YES
YES
NO
NO
YES
YES
```

### **注意**

让我们考虑一些例子：

- 第一个例子：我们从岸边跳到第一根圆木（ $0 \rightarrow 1$ ），从第一根圆木跳到第二根圆木（ $1 \rightarrow 3$ ），从第二根圆木跳到第四根圆木（ $3 \rightarrow 5$ ），从最后一根圆木跳到岸边（ $5 \rightarrow 7$ ）。所以，我们有 $0 \rightarrow 1 \rightarrow 3 \rightarrow 5 \rightarrow 7$ 。由于我们没有遇到鳄鱼，游泳距离不超过k米，所以答案是“是”。
- 第二个例子： $0 \rightarrow 1$ ，我们从第一根圆木（ $1 \rightarrow 2$ ）跳入水中，游过一个单元格到圆木（ $2 \leadsto 3$ ）， $3 \rightarrow 4 \rightarrow 5 \rightarrow 6 \rightarrow 7$ 。由于我们没有遇到鳄鱼，游泳距离不超过k米，所以答案是“是”。
- 在第三个例子中，ErnKor 需要游两个单元格“W”，但只能游一个。因此，答案是“否”。
- 第六个例子：我们从岸边跳入水中（ $0 \rightarrow 6$ ），并在水中游一个单元格（ $6 \leadsto 7$ ）。由于我们没有遇到鳄鱼，并且游了不超过 k 米，所以答案是“是”。

## 原题目

ErnKor is ready to do anything for Julen, even to swim through crocodile-infested swamps. We decided to test this love. ErnKor will have to swim across a river with a width of $ 1 $ meter and a length of $ n $ meters.

The river is very cold. Therefore, in total (that is, throughout the entire swim from $ 0 $ to $ n+1 $ ) ErnKor can swim in the water for no more than $ k $ meters. For the sake of humanity, we have added not only crocodiles to the river, but also logs on which he can jump. Our test is as follows:

Initially, ErnKor is on the left bank and needs to reach the right bank. They are located at the $ 0 $ and $ n+1 $ meters respectively. The river can be represented as $ n $ segments, each with a length of $ 1 $ meter. Each segment contains either a log 'L', a crocodile 'C', or just water 'W'. ErnKor can move as follows:

- If he is on the surface (i.e., on the bank or on a log), he can jump forward for no more than $ m $ ( $ 1 \le m \le 10 $ ) meters (he can jump on the bank, on a log, or in the water).
- If he is in the water, he can only swim to the next river segment (or to the bank if he is at the $ n $ -th meter).
- ErnKor cannot land in a segment with a crocodile in any way.

Determine if ErnKor can reach the right bank.

### 输入格式

The first line contains a single integer $ t $ ( $ 1 \le t \le 10^4 $ ) — the number of test cases.

The first line of each test case contains three numbers $ n, m, k $ ( $ 0 \le k \le 2 \cdot 10^5 $ , $ 1 \le n \le 2 \cdot 10^5 $ , $ 1 \le m \le 10 $ ) — the length of the river, the distance ErnKor can jump, and the number of meters ErnKor can swim without freezing.

The second line of each test case contains a string $ a $ of length $ n $ . $ a_i $ denotes the object located at the $ i $ -th meter. ( $ a_i \in \{ $ 'W','C','L' $ \} $ )

It is guaranteed that the sum of $ n $ over all test cases does not exceed $ 2 \cdot 10^5 $ .

### 输出格式

For each test case, output "YES" if ErnKor can pass the test, and output "NO" otherwise.

You can output the answer in any case (upper or lower). For example, the strings "yEs", "yes", "Yes", and "YES" will be recognized as positive responses.

### 样例 #1

#### 样例输入 #1

```
6
6 2 0
LWLLLW
6 1 1
LWLLLL
6 1 1
LWLLWL
6 2 15
LWLLCC
6 10 0
CCCCCC
6 6 1
WCCCCW
```

##### 样例输出 #1

```
YES
YES
NO
NO
YES
YES
```

#### 提示

Let's consider examples:

- First example: We jump from the shore to the first log ( $ 0 \rightarrow 1 $ ), from the first log to the second ( $ 1 \rightarrow 3 $ ), from the second to the fourth ( $ 3 \rightarrow 5 $ ), and from the last log to the shore ( $ 5 \rightarrow 7 $ ). So, we have $ 0 \rightarrow 1 \rightarrow 3 \rightarrow 5 \rightarrow 7 $ . Since we did not encounter a crocodile and swam no more than k meters, the answer is «YES».
- Second example: $ 0 \rightarrow 1 $ , we jump into the water from the first log ( $ 1 \rightarrow 2 $ ), swim a cell to the log ( $ 2 \leadsto 3 $ ), $ 3 \rightarrow 4 \rightarrow 5 \rightarrow 6 \rightarrow 7 $ . Since we did not encounter a crocodile and swam no more than k meters, the answer is «YES».
- In the third example, ErnKor needs to swim two cells 'W', but can only swim one. Therefore, the answer is «NO».
- Sixth example: We jump from the shore into the water ( $ 0 \rightarrow 6 $ ) and swim one cell in the water ( $ 6 \leadsto 7 $ ). Since we did not encounter a crocodile and swam no more than k meters, the answer is «YES».

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;

void Solution() // Solution一般来说不用传参
{
    int n, m, k; // n为河流的长度，m为可以跳跃的距离，k为可以游动的米数。
    cin >> n >> m >> k;
    string a; // 河流
    cin >> a;
    a = 'L' + a + 'L';              // 加上两边的陆地
    vector<int> dp(n + 2, INT_MAX); // 储存从起点到终点每一点游泳的米数，初始化为最大
    dp[0] = 0;
    for (int i = 0; i <= n + 1; i++) // 对起点到终点进行遍历
    {
        if (dp[i] == INT_MAX) // 跳过值为INT_MAX的位置，即鳄鱼的位置
            continue;
        for (int j = i + 1; j <= n + 1 && j <= i + (a[i] == 'W' ? 1 : m); j++) // 遍历当前之后可以到达的地方，注意循环终止条件
        {
            if (a[j] == 'L') // 如果是陆地或者木头，那么不用增加游泳的米数
            {
                dp[j] = min(dp[j], dp[i]);
            }
            else if (a[j] == 'W') // 如果是水下，那么需要增加1
            {
                dp[j] = min(dp[j], dp[i] + 1);
            }
            // 如果是鳄鱼，那么不能到达，仍然为INT_MAX
        }
    }
    cout << (dp[n + 1] <= k ? "YES" : "NO") << endl; // 检测最终到达时的游泳米数
}

int main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int t; // t组数据
    cin >> t;
    while (t--)
    {
        Solution();
    }
    return 0;
}
```

- 本道题采用动态规划的思路，首先初始化一个数组`vector<int> dp(n + 2, INT_MAX);`用于储存游泳的米数，初始化为最大值。
- 然后对起点到终点的每一米进行遍历，遍历当前所在位置能够到达的位置（注意循环条件），根据能够到达的位置的状况更新`dp`数组
- 最后根据`dp[n+1]`的值判断是否能到达
