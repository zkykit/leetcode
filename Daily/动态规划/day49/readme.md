
### 122买卖股票的最佳时机2
### [题目链接](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/)
### 思路：重点依旧在初始化和状态方程的书写
```
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        length = len(prices)
        if length==0:
            return 0
        dp = [[0]*2 for _ in range(length)]
        dp[0][0] = -prices[0]
        dp[0][1] = 0

        for i in range(1,length):
            #买卖分别发生一次
            dp[i][0] = max(dp[i-1][0], -prices[i])
            #买卖分别发生多次
            dp[i][0] = max(dp[i-1][0], -prices[i]+dp[i-1][1])
            dp[i][1] = max(dp[i-1][1], prices[i]+dp[i-1][0])
        return dp[-1][1]

```