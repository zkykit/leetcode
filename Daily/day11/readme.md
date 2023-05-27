## 有效的括号   
### 思路：首先是用[]表示stack，和day10不太一样，以及对于每种输入给出 对应的append；stack 里面的 top 相当于这里的[-1]
### [题目链接](https://leetcode.cn/problems/valid-parentheses/submissions/)


```
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        stack = []
        if len(s)%2 !=0:
            return False
        for i in range(len(s)):
            if s[i] == '(':
                stack.append(')')
            elif s[i] == '{':
                stack.append('}')
            elif s[i] == '[':
                stack.append(']')
            elif not stack or stack[-1]!=s[i]:
                return False
            else:#这里是为什么
                stack.pop()
        return True if not stack else False
            
```


## 删除相邻重复项
### [题目链接](https://leetcode.cn/problems/remove-all-adjacent-duplicates-in-string/submissions/)
### 思路：同样，用[]表示stack，not result 来判断是否 empty.[-1]表示和最新一个值做对比

```
class Solution(object):
    def removeDuplicates(self, s):
        """
        :type s: str
        :rtype: str
        """
        result = []
        for i in range(len(s)):
            if not result or s[i]!=result[-1]:
                result.append(s[i])
            else:
                result.pop()
        return ''.join(result)
```

## 逆波兰表达式求值150
### [题目链接](https://leetcode.cn/problems/evaluate-reverse-polish-notation/)

```
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        stack = []
        for item in tokens:
            if item not in {"+", "-", "*", "/"}:
                stack.append(item)
            else:
                first_num, second_num = stack.pop(), stack.pop()
                stack.append(
                    int(eval(f'{second_num} {item} {first_num}'))   # 第一个出来的在运算符后面
                )
        return int(stack.pop()) # 如果一开始只有一个数，那么会是字符串形式
```