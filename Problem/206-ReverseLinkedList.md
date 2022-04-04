## 206. Reverse Linked List

#LinkedlList #Recursion

Given the head of a singly linked list, reverse the list, and return the reversed list.

Example 1:

![img](https://cdn-pb.dreamoon.top/images/rev1ex1e665deac44efafad.jpg)

- Input: head = [1,2,3,4,5]
- Output: [5,4,3,2,1]

Example 2:

![img](https://cdn-pb.dreamoon.top/images/rev1ex221b0030ff5e1d26d.jpg)

- Input: head = [1,2]
- Output: [2,1]

Example 3:

- Input: head = []

- Output: []



Answer:

```python
# 迭代解法: 整个迭代的过程就把它看做从：1→2→3 到 1←2→3 到 1←2←3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: ListNode) → ListNode:
        pre = None
        cur = head

        while cur:
            temp = cur.next   # 先把原来cur.next位置存起来
            cur.next = pre    # 把头结点的 next 设为 pre，相当于反转  
            pre = cur         # 把 pre 设为 cur
            cur = temp        # 把 cur 后的元素挪上来

        return pre
```

```python
# 递归解法：“递”到最后一个节点，然后从后往前反转节点指向，参考：https://leetcode-cn.com/problems/reverse-linked-list/solution/shi-pin-jiang-jie-die-dai-he-di-gui-hen-hswxy/

# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
	def reverseList(self, head: ListNode) → ListNode:
        # 预防输入 []
        if head == None:
			return head

		# 递归终止条件是当前为空，或者下一个节点为空
		if head.next:
			# 这里的cur就是最后一个节点
			cur = self.reverseList(head.next)
			# 如果链表是 1→2→3→4→5，那么此时的cur就是5
			# 而head是4，head的下一个是5，下下一个是空
			# 所以head.next.next 就是5→4
			head.next.next = head
			# 防止链表循环，需要将head.next设置为空
			head.next = None
			# 每层递归函数都返回cur，也就是最后一个节点
			return cur
		else:
			return head
```



Notes：

**递归在性能上与迭代相比没有优势**，但迭代体现了一种**拆分**的思想——将大问题转换为小问题，并逐个解决。

*链表并非数组，每个元素之间有指向关系，注意这个特质。*



### 如何理解递归循环内（`if` 内）的逻辑？

若是 `1→2→3→4→5` 的情况，可以假设为从2往后的都已经反转好了，现在是 `1→2←3←4←5`，现在只需要把 1 和后面那些反转就行了。

```python
cur = self.reverseList(head.next);
```

可以理解成建立了一个由 2 到 1 的指向，总体来看现在是 1↔2←3←4←5

```
head.next.next = head;
```

所以还需要断开原来1 到 2 的指向：

```python
head.next = None
```



### 为什么递归方法中只更新了 `head.next.next`和`head.next ` 的值，`cur` 也发生了变化 ？

以输入 `[1,2,3,4,5]` 为例，完成“递”后第一个 return 回是[5]，这里返回的并不是一个“独立的”，“新的” 节点，而是和此前链表中的 [5] 节点**同样的内存地址**。所以，在后续更新 `head.next.next`的过程中，实际上也**同时改变了处在 `cur` 这个链表上元素的指向**，所以最后会改变 `cur`。



*P.S. 本题与 [剑指 Offer 24. 反转链表](https://leetcode-cn.com/problems/fan-zhuan-lian-biao-lcof)一致。*
