# day8 字符串
## 反转字符串
### 思路：双指针，O1空间复杂度
### [题目链接](https://leetcode.cn/problems/reverse-string/submissions/)
```
class Solution(object):
    def reverseString(self, s):
        """
        :type s: List[str]
        :rtype: None Do not return anything, modify s in-place instead.
        """
        left,right = 0,len(s)-1
        while left<right:
            s[left],s[right] = s[right],s[left]
            left+=1
            right-=1

        return s            

```

### 反转字符串2
### [题目链接](https://leetcode.cn/problems/reverse-string-ii/submissions/)
### 思路：重点在下面的 for 循环，间隔直接设成2*k
```
class Solution(object):
    def reverseStr(self, s, k):
        """
        :type s: str
        :type k: int
        :rtype: str
        """
        def reversesubstr(nums):
            left,right = 0, len(nums)-1
            while left<right:
                nums[left],nums[right] = nums[right],nums[left]
                left+=1
                right-=1
            return nums

        res = list(s)
        for i in range(0,len(s),2*k):
            res[i:i+k] = reversesubstr(res[i:i+k])
        return ''.join(res)
```

## 替换字符 %20
### 思路：双指针分别针对两个 list，对于 while 里面的 right,left 注意如何移动，也可以考虑简单方法：添加空列表：分情况往里面 append1
### [题目链接](https://leetcode.cn/problems/ti-huan-kong-ge-lcof/submissions/)

```
class Solution(object):
    def replaceSpace(self, s):
        """
        :type s: str
        :rtype: str
        """
        counter = s.count(' ')
        res = list(s)
        res.extend([' ']*counter*2)
        left,right = len(s)-1,len(res)-1
        while left>=0:
            if res[left]!=' ':
                res[right] = res[left]
                right-=1
            else:
                res[right-2:right+1]='%20'
                right-=3
            left-=1
        return ''.join(res)

```
```
class Solution:空列表法
    def replaceSpace(self, s: str) -> str:
        res = []
        for i in range(len(s)):
            if s[i] == ' ':
                res.append('%20')
            else:
                res.append(s[i])
        return ''.join(res)
```



## 翻转字符串中的单词 151
### 思路: split to list, reverse list, join
#### [题目链接](https://leetcode.cn/problems/reverse-words-in-a-string/)

```
class Solution(object):
    def reverseWords(self, s):
        """
        :type s: str
        :rtype: str
        """
        words = s.split()
        left,right = 0,len(words)-1

        while left<right:
            words[left],words[right] = words[right],words[left]
            left+=1
            right-=1

        return ' '.join(words)
```


## 左旋字符串
### [题目链接](https://leetcode.cn/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/submissions/)
### 思路:对[0：n],[n:s.zize]分别翻转，最后对整体翻转，记得翻转只能对list
```
class Solution(object):
    def reverseLeftWords(self, s, n):
        """
        :type s: str
        :type n: int
        :rtype: str
        """
        def reverseSubstr(nums):#nums-> list
            left,right = 0,len(nums)-1
            while left<right:
                nums[left],nums[right] = nums[right],nums[left]
                left+=1
                right-=1
            return nums
        res = list(s)

        res[0:n] = reverseSubstr(res[0:n])
        res[n:len(res)] = reverseSubstr(res[n:len(res)])
        res = reverseSubstr(res)
        return ''.join(res)
```