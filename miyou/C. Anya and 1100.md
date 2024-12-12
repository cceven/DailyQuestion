## C. Anya and 1100

https://codeforces.com/contest/2036/problem/C

time limit per test：3 seconds

memory limit per test：256 megabytes

While rummaging through things in a distant drawer, Anya found a beautiful string ss consisting only of zeros and ones.

Now she wants to make it even more beautiful by performing qq operations on it.

Each operation is described by two integers ii (1≤i≤|s|1≤i≤|s|) and vv (v∈{0,1}v∈{0,1}) and means that the ii-th character of the string is assigned the value vv (that is, the assignment si=vsi=v is performed).

But Anya loves the number 11001100, so after each query, she asks you to tell her whether the substring "1100" is present in her string (i.e. there exist such 1≤i≤|s|−31≤i≤|s|−3 that sisi+1si+2si+3=1100sisi+1si+2si+3=1100).

Input

The first line contains one integer tt (1≤t≤1041≤t≤104) — the number of test cases.

The first line of the test case contains the string ss (1≤|s|≤2⋅1051≤|s|≤2⋅105), consisting only of the characters "0" and "1". Here |s||s| denotes the length of the string ss.

The next line contains an integer qq (1≤q≤2⋅1051≤q≤2⋅105) — the number of queries.

The following qq lines contain two integers ii (1≤i≤|s|1≤i≤|s|) and vv (v∈{0,1}v∈{0,1}), describing the query.

It is guaranteed that the sum of |s||s| across all test cases does not exceed 2⋅1052⋅105. It is also guaranteed that the sum of qq across all test cases does not exceed 2⋅1052⋅105.

### Output

For each query, output "YES", if "1100" is present in Anya's string; otherwise, output "NO".

You can output the answer in any case (upper or lower). For example, the strings "yEs", "yes", "Yes", and "YES" will be recognized as positive responses.

Sure! Here's the translation:

## C. Anya 和 1100

**每个测试的时间限制：**3秒  
**每个测试的内存限制：**256兆字节

安雅在一个偏远的抽屉里翻找东西时，发现了一条由零和一组成的漂亮字符串 s。

现在，她想通过进行 q 次操作使其更美观。

每个操作由两个整数 i (1≤i≤|s|) 和 v (v∈{0,1}) 描述，这意味着字符串的第 i 个字符被赋值为 v（即执行赋值 si=v）。

但安雅喜欢数字 1100，因此在每个查询后，她会请你告诉她，她的字符串中是否存在子串 "1100"（即存在这样的 1≤i≤|s|−3，使得 sisi+1si+2si+3=1100）。

**输入**

第一行包含一个整数 t (1≤t≤104) —— 测试用例的数量。

每个测试用例的第一行包含字符串 s (1≤|s|≤2⋅105)，仅由字符 "0" 和 "1" 组成。这里 |s| 表示字符串 s 的长度。

下一行包含一个整数 q (1≤q≤2⋅105) —— 查询的数量。

接下来的 q 行包含两个整数 i (1≤i≤|s|) 和 v (v∈{0,1})，描述查询。

确保所有测试用例的 |s| 总和不超过 2⋅105。也确保所有测试用例的 q 总和不超过 2⋅105。

**输出**

对于每个查询，如果安雅的字符串中存在 "1100"，输出 "YES"；否则，输出 "NO"。

你可以以任何大小写输出答案（例如，字符串 "yEs"、"yes"、"Yes" 和 "YES" 都会被视为肯定回答）。

### Example

#### Input

```
4
100
4
1 1
2 0
2 0
3 1
1100000
3
6 1
7 1
4 1
111010
4
1 1
5 0
4 1
5 0
0100
4
3 1
1 1
2 0
2 1
```

#### Output

```
NO
NO
NO
NO
YES
YES
NO
NO
YES
YES
YES
NO
NO
NO
NO
```

### 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;

// 函数来计算字符串中子串 "1100" 的出现次数
int countSubstring(const string &s) // 使用引用传入常量
{
    int count = 0;
    for (size_t i = 0; i + 3 < s.size(); ++i)
    {
        if (s.substr(i, 4) == "1100")
        {
            ++count;
        }
    }
    return count;
}

int main()
{
    // 优化C++的输入输出
    ios::sync_with_stdio(false); // 这句话的作用是将C++的标准流（如cin和cout）与C的标准流（如scanf和printf）解绑定
    cin.tie(nullptr);            // 这句话的作用是将cin流和cout流分离，使它们不再自动刷新

    int t;
    cin >> t; // 对t个字符串进行操作
    while (t--)
    {
        string s; // 原始字符串
        int q;    // 操作的次数
        cin >> s >> q;

        // 计算初始子串 "1100" 的数量
        int count = countSubstring(s);
        while (q--) // 执行q次操作
        {
            int i;  // 更换第i个字符
            char v; // 更换为v
            cin >> i >> v;

            // 更新字符串和子串计数
            if (s[i - 1] != v) // 如果要更换的话
            {
                // 遍历要更改的字符的的前后长度为4的字符串
                // 因为j有可能为负数，所以不能使用“size_t”类型
                for (int j = i - 4; j <= i; ++j) // 这里的i-4其实是(i-1)-3
                {
                    // 确保索引j在合法范围内
                    if (j >= 0 && j + 3 < s.size())
                    {
                        if (s.substr(j, 4) == "1100")
                        {
                            --count; // 因为更换后有可能会减少“1100”的个数，所以先减少
                        }
                    }
                }
                s[i - 1] = v; // 更换
                // 遍历要更改的字符的的前后长度为4的字符串
                for (int j = i - 4; j <= i; ++j) // 这里的i-4其实是(i-1)-3
                {
                    // 确保索引j在合法范围内
                    if (j >= 0 && j + 3 < s.size())
                    {
                        if (s.substr(j, 4) == "1100")
                        {
                            ++count; // 如果有“1100”则count增加
                        }
                    }
                }
            }
            cout << (count > 0 ? "YES" : "NO") << endl;
        }
    }
    return 0;
}
```

- 优化C++的输入和输出

  ```cpp
      //优化C++的输入输出
      ios::sync_with_stdio(false);//这句话的作用是将C++的标准流（如cin和cout）与C的标准流（如scanf和printf）解绑定
      cin.tie(nullptr);//这句话的作用是将cin流和cout流分离，使它们不再自动刷新
  ```

  > `ios::sync_with_stdio(false);`
  >
  > ​	默认情况下，`cin`和`cout`与`scanf`和`printf`绑定在一起，以确保它们之间的混合使用不会造成问题，但会稍微减慢C++标准流的速度。
  >
  > ​	通过调用`ios::sync_with_stdio(false);`，可以提高`cin`和`cout`的性能，因为这样做消除了绑定带来的额外开销。

  > `cin.tie(nullptr);`
  >
  > ​	默认情况下，每次调用`cin`之前都会自动调用`cout.flush()`，这会导致每次输入操作都会刷新输出缓冲区。这对于某些程序是必要的，但也可能降低性能。
  >
  > ​	通过调用`cin.tie(nullptr);`，可以禁止这种自动刷新，从而提高输入输出操作的效率。

- 不能每次操作后重新检测，这样的开销太大。每次先检查是否要更改（也就是更改前的字符是否和更改后的字符相同），如果要更改，再只对更改前后有影响的字符进行检查，这样可以有效节约时间。
- `size_t`只能在一定为正数的时候使用，否则会出问题。