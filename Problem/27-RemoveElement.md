## [27. Remove Element](https://leetcode-cn.com/problems/remove-element/)

#Array #TwoPointers

Given an integer array `nums` and an integer `val`, remove all occurrences of `val` in `nums` [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm). The relative order of the elements may be changed.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the **first part** of the array `nums`. More formally, if there are `k` elements after removing the duplicates, then the first `k` elements of `nums` should hold the final result. It does not matter what you leave beyond the first `k` elements.

Return `k` *after placing the final result in the first* `k` *slots of* `nums`.

Do **not** allocate extra space for another array. You must do this by **modifying the input array [in-place](https://en.wikipedia.org/wiki/In-place_algorithm)** with O(1) extra memory. 

**Example 1:**

```
Input: nums = [3,2,2,3], val = 3
Output: 2, nums = [2,2,_,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 2.
It does not matter what you leave beyond the returned k (hence they are underscores).
```

**Example 2:**

```
Input: nums = [0,1,2,2,3,0,4,2], val = 2
Output: 5, nums = [0,1,4,0,3,_,_,_]
Explanation: Your function should return k = 5, with the first five elements of nums containing 0, 0, 1, 3, and 4.
Note that the five elements can be returned in any order.
It does not matter what you leave beyond the returned k (hence they are underscores).
```



Answer：

```python
# 暴力解法
# 通过 while 循环，匹配则弹出，不匹配则索引 + 1 且结束本次
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:        
        i = 0
        while i < len(nums):
            if nums[i] == val:
                nums.pop(i)
            else: 
                i+=1
                continue
```

由于题中说：`It does not matter what you leave beyond the returned k`，其实就意味着：`你不需要考虑数组中超出新长度后面的元素。例如，函数返回的新长度为 2 ，而 nums = [2,2,3,3] 或 nums = [2,2,0,0]，也会被视作正确答案。`

那么我们可以使用快慢指针来做这道题，把不匹配 `val` 的元素都集中到前面就行了：

![img](https://cdn-pb.dreamoon.top/images/1619009113-SlyHyv-008eGmZEly1gntrds6r59g30du09mnpd054245d4eb367195.gif)

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        i = 0	# 慢指针
        for j in range(len(nums)):	# j 为快指针
            if nums[j] != val:
                nums[i] = nums[j]
                i = i + 1
        
        return i
```



Notes：

- 注意 while 循环的 “执行规律”
- 好好读题目，如果没有题目中的 `It does not matter what you leave beyond the returned k`，我们是无法使用快慢指针做这道题的。