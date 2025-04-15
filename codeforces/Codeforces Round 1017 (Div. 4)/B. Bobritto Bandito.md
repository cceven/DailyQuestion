# [B. Bobritto Bandito](https://codeforces.com/contest/2094/problem/B)

time limit per test: 1 second

memory limit per test: 256 megabytes

input: standard input

output: standard output

In Bobritto Bandito's home town of residence, there are an infinite number of houses on an infinite number line, with houses at $\ldots, -2, -1, 0, 1, 2, \ldots$. On day $0$, he started a plague by giving an infection to the unfortunate residents of house $0$. Each succeeding day, the plague spreads to **exactly one** healthy household that is next to an infected household. It can be shown that each day the infected houses form a continuous segment.

Let the segment starting at the $l$\-th house and ending at the $r$\-th house be denoted as $[l, r]$. You know that after $n$ days, the segment $[l, r]$ became infected. Find any such segment $[l', r']$ that could have been infected on the $m$\-th day ($m \le n$).

## **Input**

The first line contains an integer $t$ ($1 \leq t \leq 100$) – the number of independent test cases.

The only line of each test case contains four integers $n$, $m$, $l$, and $r$ ($1 \leq m\leq n \leq 2000, -n \leq l \leq 0 \leq r \leq n, r-l=n$).

## **Output**

For each test case, output two integers $l'$ and $r'$ on a new line. If there are multiple solutions, output any.

## Example

### Input

```
4
4 2 -2 2
4 1 0 4
3 3 -1 2
9 8 -6 3
```

### Output

```
-1 1
0 1
-1 2
-5 3
```

### **Note**

In the first test case, it is possible that on the $1$\-st, $2$\-nd, and $3$\-rd days the interval of houses affected is $[-1,0]$, $[-1,1]$, $[-2,1]$. Therefore, $[-1,1]$ is a valid output.

## 代码

```cpp
#include<bits/stdc++.h>
using namespace std;

void solve(){
	int n, m, start, end;
	cin >> n >> m >> start >> end;
	
	int l = 0, r = 0;
	int cur_m = 0;
	while(cur_m < m){
		if(l > start){
			l--;
			cur_m++;
		}
		if(cur_m == m)break;
		
		if(r < end){
			r++;
			cur_m++; 
		}
	}
	cout << l << " " << r <<endl;
}

int main(){
	int t = 1;
	cin>>t;
	while(t--){
		solve();
	}
	return 0;
}
```

