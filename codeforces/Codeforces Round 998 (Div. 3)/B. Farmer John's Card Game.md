# B. Farmer John's Card Game

time limit per test: 2 seconds

memory limit per test: 256 megabytes

input: standard input

output: standard output

Farmer John's $n$ cows are playing a card game! Farmer John has a deck of $n \cdot m$ cards numbered from $0$ to $n \cdot m-1$. He distributes $m$ cards to each of his $n$ cows.

Farmer John wants the game to be fair, so each cow should only be able to play $1$ card per round. He decides to determine a turn order, determined by a permutation$^{\text{∗}}$ $p$ of length $n$, such that the $p_i$'th cow will be the $i$'th cow to place a card on top of the center pile in a round.

In other words, the following events happen in order in each round:

-   The $p_1$'th cow places any card from their deck on top of the center pile.
-   The $p_2$'th cow places any card from their deck on top of the center pile.
-   ...
-   The $p_n$'th cow places any card from their deck on top of the center pile.

There is a catch. Initially, the center pile contains a card numbered $-1$. In order to place a card, the number of the card must be greater than the number of the card on top of the center pile. Then, the newly placed card becomes the top card of the center pile. If a cow cannot place any card in their deck, the game is considered to be lost.

Farmer John wonders: does there exist $p$ such that it is possible for all of his cows to empty their deck after playing all $m$ rounds of the game? If so, output any valid $p$. Otherwise, output $-1$.

$^{\text{∗}}$A permutation of length $n$ contains each integer from $1$ to $n$ exactly once

## **Input**

The first line contains an integer $t$ ($1 \leq t \leq 400$) — the number of test cases.

The first line of each test case contains two integers $n$ and $m$ ($1 \leq n \cdot m \leq 2\,000$) — the number of cows and the number of cards each cow receives.

The following $n$ lines contain $m$ integers each – the cards received by each cow. It is guaranteed all given numbers (across all $n$ lines) are distinct and in the range from $0$ to $n \cdot m - 1$, inclusive.

It is guaranteed the sum of $n \cdot m$ over all test cases does not exceed $2\,000$.

## **Output**

For each test case, output the following on a new line:

-   If $p$ exists, output $n$ space-separated integers $p_1, p_2, \ldots, p_n$.
-   Otherwise, output $-1$.

## Example

### Input

```
4
2 3
0 4 2
1 5 3
1 1
0
2 2
1 2
0 3
4 1
1
2
0
3
```

### Output

```
1 2
1
-1
3 1 2 4
```

### **Note**

In the first test case, one turn order that allows all cards to be played is by having the first cow go before the second cow. The cards played will be $0\rightarrow1\rightarrow2\rightarrow3\rightarrow4\rightarrow5$.

In the second test case, there is only one cow, so having the cow play all of her cards in increasing order will empty the deck.

In the third test case, it can be shown there is no valid turn order that allows all cards to be played.

## 代码

```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
typedef long long ll;

void solve() {
  int n, m;
  cin >> n >> m;
  vector<vector<int>> cards(n, vector<int>(m));
  // 输入每头牛拥有的牌
  for (int i = 0; i < n; i++) {
    for (int j = 0; j < m; j++) cin >> cards[i][j];
  }
  // 对每头牛拥有的牌进行排序
  for (int i = 0; i < n; i++) {
    sort(cards[i].begin(), cards[i].end());
  }

  // orders用来记录从小到大的原始顺序
  vector<int> orders(n);
  iota(orders.begin(), orders.end(), 0);
  sort(orders.begin(), orders.end(),
       [&](const int &a, const int &b) { return cards[a][0] < cards[b][0]; });

  sort(cards.begin(), cards.end());
  int idx = 0;
  // 总共要进行m次循环
  for (int j = 0; j < m; j++) {
    // 每次循环要遍历n个数组
    for (int i = 0; i < n; i++) {
      if (cards[i][j] != idx) {
        cout << "-1" << endl;
        return;
      }
      idx++;
    }
  }
  // 输出原始位置
  for (int i = 0; i < n; i++) {
    if (i) cout << " ";
    cout << orders[i] + 1;
  }
  cout << endl;
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

