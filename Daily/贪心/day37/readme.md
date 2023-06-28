
### 738单调递增的数字
### [题目链接](https://leetcode.cn/problems/monotone-increasing-digits/submissions/)
### 思路：
```
class Solution(object):
    def monotoneIncreasingDigits(self, n):
        """
        :type n: int
        :rtype: int
        """
        n=list(str(n))
        # flag = len(n)
        for i in range(len(n)-1,0,-1):
            if n[i-1]>n[i]:#前一位比后一位大情况下-1
                n[i-1] = str(int(n[i-1])-1)
                # flag=i  
                for j in range(i,len(n)):#后面全部变为999
                    n[j] = '9'
        return int(''.join(n))

```