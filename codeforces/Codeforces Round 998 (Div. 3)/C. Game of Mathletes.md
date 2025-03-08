# C. Game of Mathletes

time limit per test: 2 seconds

memory limit per test: 256 megabytes

input: standard input

output: standard output

Alice and Bob are playing a game. There are $n$ (**$n$ is even**) integers written on a blackboard, represented by $x_1, x_2, \ldots, x_n$. There is also a given integer $k$ and an integer score that is initially $0$. The game lasts for $\frac{n}{2}$ turns, in which the following events happen sequentially:

-   Alice selects an integer from the blackboard and erases it. Let's call Alice's chosen integer $a$.
-   Bob selects an integer from the blackboard and erases it. Let's call Bob's chosen integer $b$.
-   If $a+b=k$, add $1$ to score.

Alice is playing to minimize the score while Bob is playing to maximize the score. Assuming both players use optimal strategies, what is the score after the game ends?

## **Input**

The first line contains an integer $t$ ($1 \leq t \leq 10^4$) — the number of test cases.

The first line of each test case contains two integers $n$ and $k$ ($2 \leq n \leq 2\cdot 10^5, 1 \leq k \leq 2\cdot n$, $n$ is even).

The second line of each test case contains $n$ integers $x_1,x_2,\ldots,x_n$ ($1 \leq x_i \leq n$) — the integers on the blackboard.

It is guaranteed that the sum of $n$ over all test cases does not exceed $2\cdot 10^5$.

## **Output**

For each test case, output the score if both players play optimally.

## Example

### Input

```
4
4 4
1 2 3 2
8 15
1 2 3 4 5 6 7 8
6 1
1 1 1 1 1 1
16 9
3 1 4 1 5 9 2 6 5 3 5 8 9 7 9 3
```

### Output

```
2
1
0
4
```

**Note**

In the first test case, one way the game may go is as follows:

-   Alice selects $1$ and Bob selects $3$. The score increases as $1+3=4$. Now the two integers remaining on the blackboard are $2$ and $2$.
-   Alice and Bob both select $2$. The score increases as $2+2=4$.
-   The game ends as the blackboard now has no integers.

In the third test case, it is impossible for the sum of Alice and Bob's selected integers to be $1$, so we answer $0$.

**Note that this is just an example of how the game may proceed for demonstration purposes. This may not be Alice or Bob's most optimal strategies.**

## 代码

```cpp

```

