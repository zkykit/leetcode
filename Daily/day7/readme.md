# day7
## 四数相加（等于0） 454
### 思路：分别对 ab,cd进行遍历，使用 hashmap，用 dict 初始化
### [题目链接](https://leetcode.cn/problems/4sum-ii/submissions/)
### 时间复杂度 O（2n^2）
```
class Solution(object):
    def fourSumCount(self, nums1, nums2, nums3, nums4):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :type nums3: List[int]
        :type nums4: List[int]
        :rtype: int
        """
        hashmap = dict()
        for a in nums1:
            for b in nums2:
                if a+b in hashmap:
                    hashmap[a+b] +=1
                else:
                    hashmap[a+b] = 1
        count = 0
        for c in nums3:
            for d in nums4:
                target = 0-(c+d)
                if target in hashmap:
                    count += hashmap[target]
        return count
```


## 赎金信 判断两个字符串的包含关系
### 思路：hasnmap,注意在第二个字符串提取value 使用hashmap.get(x)
### [题目链接](https://leetcode.cn/problems/ransom-note/submissions/)

```
class Solution(object):
    def canConstruct(self, ransomNote, magazine):
        """
        :type ransomNote: str
        :type magazine: str
        :rtype: bool
        """

        hashmap = dict()
        for x in magazine:
            if x in hashmap:
                hashmap[x] +=1
            else:
                hashmap[x] = 1

        for x in ransomNote:
            value = hashmap.get(x)
            if not value:
                return False
            else:
                hashmap[x] -=1
        return True

```

### 三数之和
### 思路：双指针，对于 left和 right 边界问题要注意(不用哈希表是因为这里复杂，考虑到剪枝.)
### [题目链接](https://leetcode.cn/problems/3sum/submissions/)
### [思路画图](https://github.com/zkykit/leetcode/blob/main/IMG/%E4%B8%89%E6%95%B0%E4%B9%8B%E5%92%8C.JPG)
```
class Solution(object):
    def threeSum(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        result = []
        nums.sort()
        
        for i in range(len(nums)):
            if nums[i]>0:
                return result
            if i >0 and nums[i] == nums[i-1]:#去重
                continue
            
            left = i+1
            right = len(nums)-1
            while left<right:
                sum = nums[i]+nums[left]+nums[right]
                if sum>0:
                    right-=1
                elif sum<0:
                    left+=1
                else:
                    result.append([nums[i],nums[left],nums[right]])
                    while left<right and nums[right] == nums[right-1]:#不懂为什么这里多余吗,因为下面有-1
                        right-=1
                    while left<right and nums[left] == nums[left+1]:
                        left+=1
                    right-=1
                    left+=1
        return result
            

```