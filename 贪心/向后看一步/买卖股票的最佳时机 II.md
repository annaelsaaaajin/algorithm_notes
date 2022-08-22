# LeetCode 122. 买卖股票的最佳时机 II
[LeetCode 122. 买卖股票的最佳时机 II](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/)

# 解题思路
遍历一次数组，低进高出，把正的价格差相加起来就是最终利润

递增，如`[1,2,3]`，那么 $1$ 买 $3$ 卖 与 每天都买入卖出 等价
递减，如`[3,2,1]`，赚钱是赚不了的
先高再低，如`[1,3,2]`，那么只能在 $1$ 买 $3$ 卖捞一笔
先低再高，如`[2,1,3]`，那么同样只能在$1$ 买 $3$ 卖捞一笔

### Code
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int ans = 0;
        for (int i = 1; i < prices.size(); i ++)
            if (prices[i] - prices[i - 1] > 0)
                ans += prices[i] - prices[i - 1];
        return ans;
    }
};
```