## [977. Squares of a Sorted Array](https://leetcode-cn.com/problems/squares-of-a-sorted-array/)

#Array #TwoPointers #Sorting

Given an integer array `nums` sorted in **non-decreasing** order, return *an array of **the squares of each number** sorted in non-decreasing order*.

**Example 1:**

```
Input: nums = [-4,-1,0,3,10]
Output: [0,1,9,16,100]
Explanation: After squaring, the array becomes [16,1,0,9,100].
After sorting, it becomes [0,1,9,16,100].
```

**Example 2:**

```
Input: nums = [-7,-3,2,3,11]
Output: [4,9,9,49,121]
```

 

Answer：

```python
# 最简单的，先遍历元素做平方，然后做排序
# 这种做法会超过运行时间限制，无法通过。
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        # 先遍历元素，并平方
        for i in range(len(nums)):
            nums[i] = nums[i] * nums[i]

        # 再排序输出
        res = []
        for j in range(len(nums)):
            val,idx = nums[0],0
            for k in range(1, len(nums)):
                if nums[k] < val:
                    val = nums[k]
                    idx = k

            nums.pop(idx)
            res.append(val)

        return res
```

由于题目中说给定的 nums 是 non-decreasing 的，所以我们可以直接比较左右两边的数，把更大的放入新数组中即可，那么使用双指针是个不错的选择：

![977.有序数组的平方.gif](https://pic.leetcode-cn.com/1631932242-BViXlX-977.有序数组的平方.gif)

```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        l, r = 0, len(nums) - 1 # 设置 nums 的左右两个指针

        # 新建一个数组接收结果
        res = [0] * len(nums)
        # 数组的索引，用于记录存放的位置
        resIndex = len(res) - 1

        # 注意，这里必须是 <=，如果只是 < 则会少比较一次（与二分查找不同）
        while l <= r:
            if nums[l] * nums[l] > nums[r] * nums[r]:
                res[resIndex] = nums[l] * nums[l]
                l = l + 1
            else:
                res[resIndex] = nums[r] * nums[r]
                r = r - 1

            resIndex -= 1

        return res
```

