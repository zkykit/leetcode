
## 用栈实现队列
### [题目链接](https://leetcode.cn/problems/implement-queue-using-stacks/submissions/)
### 思路：不同的函数功能,需要两个stack
```
class MyQueue(object):

    def __init__(self):
        self.stack_in = []
        self.stack_out = []
    def push(self, x):
        """
        :type x: int
        :rtype: None
        """
        self.stack_in.append(x)
    def pop(self):
        """
        :rtype: int
        """
        if self.empty():
            return None
        if self.stack_out:
            return self.stack_out.pop()
        else:
            for i in range(len(self.stack_in)):
                self.stack_out.append(self.stack_in.pop())
            return self.stack_out.pop()
    def peek(self):
        """
        :rtype: int
        """
        ans = self.pop()
        self.stack_out.append(ans)
        return ans

    def empty(self):
        """
        :rtype: bool
        """
        return not(self.stack_in or self.stack_out)

 
```

## 用列实现栈
### 思路: 注意 top 是用来获取front 元素, 一个deque 完成
### [题目链接](https://leetcode.cn/problems/implement-stack-using-queues/submissions/)
### ![image](https://github.com/zkykit/leetcode/blob/main/IMG/%E9%98%9F%E5%88%97%E5%AE%9E%E7%8E%B0%E6%A0%88.jpg)
```
class MyStack(object):

    def __init__(self):
        self.que = deque()

    def push(self, x):
        """
        :type x: int
        :rtype: None
        """
        self.que.append(x)
    def pop(self):
        """
        :rtype: int
        """
        if self.empty():
            return None
        for i in range(len(self.que)-1):
            self.que.append(self.que.popleft())
        return self.que.popleft()
    def top(self):
        """
        :rtype: int
        """
        if self.empty():
            return None
        return self.que[-1]
    def empty(self):
        """
        :rtype: bool
        """
        return not self.que
```