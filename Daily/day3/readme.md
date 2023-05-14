
## 移除链表元素 Leetcode 203 
## 题目链接[https://leetcode.cn/problems/remove-linked-list-elements/]
### 时间复杂度: O(n)
### 空间复杂度: O(1)
### 思路:画图，
```
class Solution(object):
    def removeElements(self, head, val):
        """
        :type head: ListNode
        :type val: int
        :rtype: ListNode
        """
        dummyhead = ListNode(next=head)
        cur = dummyhead
        while cur.next:
            if cur.next.val == val:
                cur.next = cur.next.next
            else:
                cur = cur.next
            
        return dummyhead.next
```
## 设计链表Leetcode 707
## 题目链接 [https://leetcode.cn/problems/design-linked-list/]
### 时间复杂度: 涉及 index 的相关操作为 O(index), 其余为 O(1)
### 空间复杂度: O(n)

```
# 单链表
class Node(object):
    def __init__(self, x=0):
        self.val = x
        self.next = None

class MyLinkedList(object):

    def __init__(self):
        self.head = Node()
        self.size = 0 # 设置一个链表长度的属性，便于后续操作，注意每次增和删的时候都要更新

    def get(self, index):
        """
        :type index: int
        :rtype: int
        """
        if index < 0 or index >= self.size:
            return -1
        cur = self.head.next
        while(index):
            cur = cur.next
            index -= 1
        return cur.val

    def addAtHead(self, val):
        """
        :type val: int
        :rtype: None
        """
        new_node = Node(val)
        new_node.next = self.head.next
        self.head.next = new_node
        self.size += 1

    def addAtTail(self, val):
        """
        :type val: int
        :rtype: None
        """
        new_node = Node(val)
        cur = self.head
        while(cur.next):
            cur = cur.next
        cur.next = new_node
        self.size += 1

    def addAtIndex(self, index, val):
        """
        :type index: int
        :type val: int
        :rtype: None
        """
        if index < 0:
            self.addAtHead(val)
            return
        elif index == self.size:
            self.addAtTail(val)
            return
        elif index > self.size:
            return

        node = Node(val)
        pre = self.head
        while(index):
            pre = pre.next
            index -= 1
        node.next = pre.next
        pre.next = node
        self.size += 1
        
    def deleteAtIndex(self, index):
        """
        :type index: int
        :rtype: None
        """
        if index < 0 or index >= self.size:
            return
        pre = self.head
        while(index):
            pre = pre.next
            index -= 1
        pre.next = pre.next.next
        self.size -= 1
```

## 反转列表 Leetcode 206
## 题目链接[https://leetcode.cn/problems/reverse-linked-list/]
### 思路：没有使用双指针，而是根据 cur,pre,head 这几个变量的关系，进行赋值，注意 temp,可以画图比较清晰。
```
class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        cur = head
        pre = None
        while cur:
            temp = cur.next
            cur.next = pre
            pre = cur
            cur = temp
        return pre
```