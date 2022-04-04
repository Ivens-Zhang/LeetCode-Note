## [剑指 Offer 22. 链表中倒数第k个节点](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/)

#LinkedlList #TwoPointers

输入一个链表，输出该链表中倒数第k个节点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。

例如，一个链表有 `6` 个节点，从头节点开始，它们的值依次是 `1、2、3、4、5、6`。这个链表的倒数第 `3` 个节点是值为 `4` 的节点。

 

**示例：**

```tex
给定一个链表: 1->2->3->4->5, 和 k = 2.

返回链表 4->5.
```

Answer：

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def getKthFromEnd(self, head: ListNode, k: int) -> ListNode:
        # 拷贝一个链表，防止在计算长度的时候破坏原来的链表
        tmp = ListNode(0)
        tmp = head
        # 先知道链表长度
        count = 0
        while tmp:
            count = count + 1
            tmp = tmp.next

        times = count - k   # 从头结点到目标节点所需 next 的次数
        for i in range(0,times):
            head = head.next
        return head
```

```python
# 双指针法★
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def getKthFromEnd(self, head: ListNode, k: int) -> ListNode:
        fast, slow = head, head

        # 这步是要让 fast 和 slow 间隔 k 个长度
        while fast and k > 0:
            fast, k = fast.next, k - 1

        # 这步是让 fast 和 slow 一起向后走，直到 fast 到头
        while fast:
            fast,slow = fast.next,slow.next
        
        return slow
```







