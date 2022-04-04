## [215. Kth Largest Element in an Array](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/)

Given an integer array `nums` and an integer `k`, return *the* `kth` *largest element in the array*.

Note that it is the `kth` largest element in the sorted order, not the `kth` distinct element.

**Example 1:**

```
Input: nums = [3,2,1,5,6,4], k = 2
Output: 5
```

**Example 2:**

```
Input: nums = [3,2,3,1,2,4,5,5,6], k = 4
Output: 4
```

 

Answer：

先使用最基础的三种排序：

- 选择排序
- 插入排序
- 冒泡排序

*其中冒泡排序会超过限定运行时长，所以未能通过。*

后续可以使用堆排序、快速排序等方法实现，待补充。

```python
# 选择排序
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        # select sort
        res = []
        for i in range(0, len(nums)):
            val, idx = nums[0], 0
            for j in range(1, len(nums)):
                if nums[j] < val:
                    val = nums[j]
                    idx = j
            nums.pop(idx)
            res.append(val)

        
        return res[len(nums) - k]
```

```python
# 插入排序
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        # insertion sort
        for i in range(1, len(nums)):
            for j in range(0, i):
                if nums[i] < nums[j]:
                    tmp = nums[i]
                    nums.pop(i)
                    nums.insert(j, tmp)
                    break
        

        return nums[len(nums) - k]
```





















