## [21. Merge Two Sorted Lists](https://leetcode-cn.com/problems/merge-two-sorted-lists/)

#LinkedlList #TwoPointers #Recursion

You are given the heads of two sorted linked lists `list1` and `list2`.

Merge the two lists in a one **sorted** list. The list should be made by splicing together the nodes of the first two lists.

Return *the head of the merged linked list*.

 

**Example 1:**

<img src="https://cdn-pb.dreamoon.top/images/merge_ex163ec25d9c43e3bd7.jpg" alt="img" style="zoom:67%;" />

- Input: list1 = [1,2,4], list2 = [1,3,4]

- Output: [1,1,2,3,4,4]

**Example 2:**

- Input: list1 = [], list2 = []

- Output: []

**Example 3:**

- Input: list1 = [], list2 = [0]

- Output: [0]



Answer：

```python
# 双指针解法
# 思路：为两个链表各设置一个指针，挨个将元素添加到 prehead 后。
# 可参考视频：https://www.youtube.com/watch?v=XIdigk956u0&ab_channel=NeetCode
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:

        # 创建一个初始节点为 -1 的链表
        prehead = ListNode(-1)
        prev = prehead

        while list1 and list2:
            if list1.val <= list2.val:
                prev.next = list1
                list1 = list1.next
            else:
                prev.next = list2
                list2 = list2.next
            prev = prev.next

        # 会有一条链表先到末尾跳出循环，这时让 prev 的 next 指向剩下的另一条链表
        prev.next = list1 if list1 is not None else list2
        
        return prehead.next
```

```python
# 递归解法
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:

        if list1 is None: return list2
        if list2 is None: return list1

        if list1.val <= list2.val:
            list1.next = self.mergeTwoLists(list1.next, list2)
            return list1 # 这里 return 是什么意思, 是从后往前返回的尾部链表，然后返回给上一个进入的递归中
        else:
            list2.next = self.mergeTwoLists(list1, list2.next)
            return list2
```



Notes：

这题递归解法的确较难。



