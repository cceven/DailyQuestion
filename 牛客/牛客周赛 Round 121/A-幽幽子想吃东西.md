[幽幽子想吃东西](https://ac.nowcoder.com/acm/contest/124143/A)
![[Pasted image 20251214130527.png]]
```cpp
#include <bits/stdc++.h>
#define endl "\n"
using namespace std;
using ll = long long;
#define int ll

void solve() {
  int a,b,c,n;
  cin>>a>>b>>c>>n;
  int ans=a*n-(n<=b?c:0);
  cout<<ans<<endl;
}

signed main() {
  ios::sync_with_stdio(false);
  cin.tie(nullptr);
  int t = 1;
  // cin >> t;
  while (t--) solve();
  return 0;
}
```