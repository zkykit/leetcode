### 122买卖股票
###
###
```
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        result = 0
        for i in range(len(prices)-1):
            result += max(prices[i+1]-prices[i],0)
        return result
```

### 55跳跃游戏
### [题目链接](https://leetcode.cn/problems/jump-game/submissions/)
### 思路：32行重要，前提是要求索引在当前覆盖范围之内，这样可以继续往下一步走，想清楚这里是关键
```
class Solution(object):
    def canJump(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        n = len(nums)
        if len(nums) == 1:
            return True
        sum_=0
        for i,b in enumerate(nums):
            if i <= sum_:
                sum_ = max(i+b,sum_)
                if sum_ >= n-1:
                    return True
        return False
```

### 45跳跃游戏
### [题目链接](https://leetcode.cn/problems/jump-game-ii/submissions/)
### 思路：求最小step，在这里需要对索引和当前 index进行限制
```
class Solution(object):
    def jump(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums)==1:
            return 0
        cur_index, next_index = 0,0
        step = 0
        for index in range(len(nums)):
            next_index = max(next_index,nums[index]+index)
            if index == cur_index:
                step+=1
                cur_index = next_index
                if next_index>=len(nums)-1:#说明此时到达了倒数第二个点
                    break
        return step

```