### K次取反后最大数组和 1005
### [题目链接](https://leetcode.cn/problems/maximize-sum-of-array-after-k-negations/)
### 思路：注意第二个 if 表达的含义：当 k 不为0的情况
```

class Solution(object):
    def largestSumAfterKNegations(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        nums.sort(key=lambda x:abs(x), reverse = True)
        for i in range(len(nums)):
            if nums[i]<0 and k>0:
                nums[i] *= -1
                k-=1
        if k%2 == 1:
            nums[-1] *= -1
        return sum(nums)
            

```

### 134 加油站
### [题目链接](https://leetcode.cn/problems/gas-station/submissions/)
### 思路：注意当 startIndex加一的时候需要将 curSum 重置
```
class Solution(object):
    def canCompleteCircuit(self, gas, cost):
        """
        :type gas: List[int]
        :type cost: List[int]
        :rtype: int
        """
        curSum,totalSum = 0,0
        startIndex = 0
        for i in range(len(gas)):
            curSum += gas[i]-cost[i]
            totalSum += gas[i]-cost[i]
            if curSum<0:
                startIndex = i+1
                curSum = 0
        if totalSum<0:
            return -1
        return startIndex
```