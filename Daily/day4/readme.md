# 代码随想录训练营第4天 | Leetcode 24 两两交换列表节点，Leetcode  

## 题目[https://leetcode.cn/problems/swap-nodes-in-pairs/]
### 思路：设置两个 temp变量以及12互换跟冒泡排序原理一样；以及 while 条件分成奇偶来讨论,对顺序有要求

### 时间复杂度：O(n) ；空间复杂度：O(1)
```
class Solution(object):
    def swapPairs(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        dummyhead = ListNode(next,head)
        cur = dummyhead
        while cur.next!=None and cur.next.next!=None:
            temp = cur.next
            temp1 = cur.next.next.next
            #12互换
            cur.next = cur.next.next
            cur.next.next = temp
            #1指向3
            temp.next = temp1
            cur = cur.next.next
        return dummyhead.next
```
## Leetcode 24 删除倒数第 n 个节点 Leetcode 19
## 题目[https://leetcode.cn/problems/remove-nth-node-from-end-of-list/submissions/]
### 思路： 对于 fast,slow 的位置要清晰，如何移动，判断条件是什么
### ![image]()
### 时间复杂度: O(n);空间复杂度: O(1)


```
class Solution(object):
    def removeNthFromEnd(self, head, n):
        """
        :type head: ListNode
        :type n: int
        :rtype: ListNode
        """
        dummyhead = ListNode(next,head)
        slow = fast = dummyhead
        while n>=0:#移动 fast 指针
            fast = fast.next
            n-=1
        while fast != None:#同时移动双指针
            fast = fast.next
            slow = slow.next
        slow.next = slow.next.next#删除命令
        return dummyhead.next
```

## Leetcode 02.07 链表相交
## 链接[https://leetcode.cn/problems/intersection-of-two-linked-lists-lcci/]
### 思路：分别从 A,B段走三段，最终路径一定相等。画图比较清晰
### 时间复杂度：O(n+m)；空间复杂度O(1)。

```
class Solution(object):
    def getIntersectionNode(self, headA, headB):
        """
        :type head1, head1: ListNode
        :rtype: ListNode
        """
    
        if not headA or not headB:
            return None
        curA = headA
        curB = headB
        #分别从 A,B段走三段，最终路径一定相等
        while curA!=curB:
            curA=curA.next if curA else headB
            curB=curB.next if curB else headA
        return curA
```
## Leetcode 环形链表142
## 题目[https://leetcode.cn/problems/linked-list-cycle-ii/submissions/]
### 思路：先找到环，再找交点;分别定义快慢和 index 指针。
### ![image](https://github.com/zkykit/leetcode/blob/main/IMG/%E7%8E%AF%E5%BD%A2%E9%93%BE%E8%A1%A8.jpg) 
### 时间复杂度：；空间复杂度。
```
class Solution(object):
    def detectCycle(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        fast = head
        slow = head
        while fast!=None and fast.next!=None:
            fast = fast.next.next
            slow = slow.next
            #找到环，看其是否存在
            if fast==slow:
                index1 = fast
                index2 = head
                #找到线和环的交点
                while index1!=index2:
                    index1 = index1.next
                    index2 = index2.next
                return index1
        return None
```