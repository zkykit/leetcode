# 代码随想录训练营第5天 哈希表| Leetcode 242有效的字母异位 ,
### 题目链接[https://leetcode.cn/problems/valid-anagram/submissions/]
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
### 题目链接[https://leetcode.cn/problems/intersection-of-two-arrays/submissions/]
### 思路： 哈希表。建立 set，nums1-> unordered_set。与nums2比较
### 时间复杂度O(n)：；空间复杂度O(1)。
## ![image]()
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
