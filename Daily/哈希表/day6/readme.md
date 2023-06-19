# 代码随想录训练营第5天 哈希表| Leetcode 242有效的字母异位 ,
### [有效的字母异位](https://leetcode.cn/problems/valid-anagram/submissions/)
### 思路:用 ord 表示 ASCII码，先加再减，对于字母范围用26；
### 时间复杂度：O(n)；空间复杂度：O(1)

```
class Solution(object):
    def isAnagram(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        record = [0] * 26
        for i in s:
            record[ord(i)-ord('a')]+=1
        for i in t:
            record[ord(i)-ord('a')]-=1
        for i in range(26):
            if record[i]!=0:
                return False
        return True
```

## Leetcode 349 两个数组的交集 
### [两个数组的交集](https://leetcode.cn/problems/intersection-of-two-arrays/submissions/)
### 思路： 哈希表。建立 set，nums1-> unordered_set。与nums2比较
### 时间复杂度O(n)；空间复杂度O(1)。
## ![image](https://github.com/zkykit/leetcode/blob/main/IMG/%E4%B8%A4%E4%B8%AA%E6%95%B0%E7%BB%84%E4%BA%A4%E9%9B%86.png)
```
class Solution(object):
    def intersection(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: List[int]
        """
        val_dict = {}
        ans = []
        for num in nums1:
            val_dict[num] = 1
        for num in nums2:
            if num in val_dict.keys() and val_dict[num]==1:
                ans.append(num)
                val_dict[num]=0
        return ans
```


## Leetcode 202快乐数
## [快乐数]（https://leetcode.cn/problems/happy-number/submissions/)
### 思路：判断是否在另一堆数里面，用 set，注意区分%，//
```
class Solution(object):
    def isHappy(self, n):
        """
        :type n: int
        :rtype: bool
        """
        def cal_happy(num):
            sum_ = 0
            while num:
                sum_ += (num%10)**2
                num = num//10
            return sum_ 
        record = set()
        
        while True:
            n = cal_happy(n)
            if n == 1:
                return True
            
            if n in record:
                return False
            else:
                record.add(n)
```
## Leetcode 两数之和 1
## [两数之和](https://leetcode.cn/problems/two-sum/submissions/)
### 思路 用map，因为涉及到数组下标,注意如何将元素及索引添加到 map

```
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        record = dict()
        for i in range(len(nums)):
            s=target-nums[i]
            if s in record:
                return [record[s],i]
            #将当前元素及其索引添加到record字典中。
            record[nums[i]] = i
        return []

```