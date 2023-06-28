
### 509斐波那契数列
### [题目链接](https://leetcode.cn/problems/fibonacci-number/submissions/)
### 思路：注意创建 dp数组的方式；其次注意 for 循环的右边界
```
class Solution(object):
    def fib(self, n):
        """
        :type n: int
        :rtype: int
        """
        if n is 0:
            return 0
        #创建 dp table
        dp = [0]*(n+1)
        #初始化
        dp[0] = 0
        dp[1] = 1
        for i in range(2,n+1):
            dp[i] = dp[i-1]+dp[i-2]
        return dp[n]
```

### 爬楼梯
### [题目链接](https://leetcode.cn/problems/climbing-stairs/submissions/)
### 思路:注意初始化是从第三项开始，因为没有 dp[0]也就是没有第0层
```
class Solution(object):
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        #特殊情况
        if n<=1:
            return n
        #创建数组
        dp = [0]*(n+1)
        dp[1] = 1
        dp[2] = 2
        for i in range(3,n+1):
            dp[i] = dp[i-1]+dp[i-2]
        return dp[n]
```

### 746使用最小花费爬楼梯
### [题目链接](https://leetcode.cn/problems/min-cost-climbing-stairs/submissions/)
### 思路：注意初始化这里从0或者1开始都可以
```
class Solution(object):
    def minCostClimbingStairs(self, cost):
        """
        :type cost: List[int]
        :rtype: int
        """
        dp = [0]*(len(cost)+1)
        dp[0] = 0
        dp[1] = 0
        for i in range(2,len(cost)+1):
            dp[i] = min(dp[i-1]+cost[i-1],dp[i-2]+cost[i-2])
        return dp[len(cost)]
```