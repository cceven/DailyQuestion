# **7-96 Wifi密码**

分数 15

作者 CHEN, Yue

单位 浙江大学

下面是微博上流传的一张照片：“各位亲爱的同学们，鉴于大家有时需要使用 wifi，又怕耽误亲们的学习，现将 wifi 密码设置为下列数学题答案：A-1；B-2；C-3；D-4；请同学们自己作答，每两日一换。谢谢合作！！~”—— 老师们为了促进学生学习也是拼了…… 本题就要求你写程序把一系列题目的答案按照卷子上给出的对应关系翻译成 wifi 的密码。这里简单假设每道选择题都有 4 个选项，有且只有 1 个正确答案。

![4ea7ee49-5155-49e1-977d-7465359db177](https://gitee.com/chen-houchao/images/raw/master/img/20250224230556014.png)

## 输入格式：

输入第一行给出一个正整数 N（≤ 100），随后 N 行，每行按照 `编号-答案` 的格式给出一道题的 4 个选项，`T` 表示正确选项，`F` 表示错误选项。选项间用空格分隔。

## 输出格式：

在一行中输出 wifi 密码。

## 输入样例：

```in
8
A-T B-F C-F D-F
C-T B-F A-F D-F
A-F D-F C-F B-T
B-T A-F C-F D-F
B-F D-T A-F C-F
A-T C-F B-F D-F
D-T B-F C-F A-F
C-T A-F B-F D-F
```

## 输出样例：

```out
13224143
```

代码长度限制

16 KB

时间限制

400 ms

内存限制

64 MB

栈限制

8192 KB

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;

void solve() {
  int N;
  cin >> N;
  cin.ignore();
  string ans;
  for (int i = 0; i < N; i++) {
    string in_ans;
    getline(cin, in_ans);
    auto pos = in_ans.find("T");
    ans += to_string(in_ans[pos - 2] - 'A' + 1);
  }
  cout << ans;
}

int main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);

  solve();
  return 0;
}
```

