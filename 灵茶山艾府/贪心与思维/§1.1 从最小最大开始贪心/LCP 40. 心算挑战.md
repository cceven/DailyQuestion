# [LCP 40. 心算挑战](https://leetcode.cn/problems/uOAnQW/)

「力扣挑战赛」心算项目的挑战比赛中，要求选手从 `N` 张卡牌中选出 `cnt` 张卡牌，若这 `cnt` 张卡牌数字总和为偶数，则选手成绩「有效」且得分为 `cnt` 张卡牌数字总和。 给定数组 `cards` 和 `cnt`，其中 `cards[i]` 表示第 `i` 张卡牌上的数字。 请帮参赛选手计算最大的有效得分。若不存在获取有效得分的卡牌方案，则返回 0。

## **示例 1：**

> 输入：`cards = [1,2,8,9], cnt = 3`
>
> 输出：`18`
>
> 解释：选择数字为 1、8、9 的这三张卡牌，此时可获得最大的有效得分 1+8+9=18。

## **示例 2：**

> 输入：`cards = [3,3,1], cnt = 1`
>
> 输出：`0`
>
> 解释：不存在获取有效得分的卡牌方案。

## **提示：**

- `1 <= cnt <= cards.length <= 10^5`
- `1 <= cards[i] <= 1000`

## 代码

```cpp
class Solution {
public:
    int maximumScore(vector<int>& cards, int cnt) {
        int n = cards.size();
        sort(cards.begin(), cards.end(), greater<int>());
        int sum = reduce(cards.begin(), cards.begin() + cnt);
        // 如果是偶数，那么直接返回结果
        if (!(sum & 1))
            return sum;

        // 从未选定的数字中选择一个奇偶性不同的数字进行替换
        auto replaceNum = [&](const int& num) -> int {
            for (int i = cnt; i < n; i++) {
                if ((num & 1) != (cards[i] & 1)) {
                    return sum - num + cards[i];
                }
            }
            return 0;
        };

        // 首先更换掉选定数组的最后一个数字进行更换
        int ans = replaceNum(cards[cnt - 1]);
        // 然后选择最后一个数字前面的数字进行更换，取最大值
        for (int i = cnt - 2; i >= 0; i--) {
            if ((cards[cnt - 1] & 1) != (cards[i] & 1)) {
                ans = max(ans, replaceNum(cards[i]));
                break;
            }
        }
        return ans;
    }
};
```

- 判断两个数字奇偶性是否相同可以使用`a % 2 == b % 2`，也可以使用`a & 1 == b & 1`