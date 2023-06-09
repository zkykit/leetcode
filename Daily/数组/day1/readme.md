# 代码随想录训练营第一天 | Leetcode 704 二分查找，Leetcode 35 去除元素

## 题目链接
[https://leetcode.cn/problems/binary-search/]

## 思路：
### 要注意的点是根据不同的开闭条件，确定初始left,right的值（我自己出错的点），以及进行条件判断后，对于 left,right 的赋值。建议这里可以画一下图容易理解。

## 时间复杂度：O(log n),空间复杂度：O(1)。
## 704 二分查找


```
class Solution(object):
    def search(self, nums, target):    
        #左右均闭 []
        left,right = 0,len(right)-1
        while left<=right:
            middle = (left+right)//2
            if nums[middle]<target:
                left = middle+1
            elif nums[middle]>target:
                right = middle-1
            else:
                return middle
        return -1
        #左闭右开 [)
        left,right = 0,len(right)
        while left<=right:
            middle = (left+right)//2
            if nums[middle]<target:
                left = middle+1
            elif nums[middle]>target:
                right = middle
            else:
                return middle
        return -1

```

## 题目链接
[https://leetcode.cn/problems/remove-element/]
## 思路
### 快慢指针法：这道题的思想主要是两个指针的快慢问题，fast保持每次向右移动一位，而 slow 只在 if 条件成立下才移动，最后输出 slow。
### 暴力法：没有太多可说的，注意数组向左平移的写法，左右边界均-1.

## 时间复杂度：O(n),空间复杂度：O(1)。
## 代码35 去除元素

```

class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        #快慢指针
        fast = 0
        slow = 0
        size = len(nums)
        while fast<size:
            if nums[fast]!=val:
                nums[slow] = nums[fast]
                slow+=1
            fast+=1
        return slow

```

```

class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        i, l = 0, len(nums)
        while i < l:
            if nums[i] == val: # 找到等于目标值的节点
                for j in range(i+1, l): # 移除该元素，并将后面元素向前平移
                    nums[j - 1] = nums[j]
                l -= 1
                i -= 1
            i += 1
        return l
```
