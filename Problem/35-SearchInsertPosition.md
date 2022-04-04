## [35. Search Insert Position](https://leetcode-cn.com/problems/search-insert-position/)

#Array #BinarySearch

```tex
Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with O(log n) runtime complexity.

 

Example 1:
Input: nums = [1,3,5,6], target = 5
Output: 2

Example 2:
Input: nums = [1,3,5,6], target = 2
Output: 1

Example 3:
Input: nums = [1,3,5,6], target = 7
Output: 4
 

Constraints:

1 <= nums.length <= 104
-104 <= nums[i] <= 104
nums contains distinct values sorted in ascending order.
-104 <= target <= 104

```



Answer:

```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums) - 1

        while left <= right:
            middle = (left + right) // 2
            if nums[middle] == target:
                return middle
            elif nums[middle] < target:
                left = middle + 1
            else:
                right = middle - 1
            
        return left
```



Notes:

> Q1: 与 [704](https://leetcode-cn.com/problems/binary-search) 在有何不同之处？
>
> - 着重需要思考如果数组内不存在 `target` 该如何确定插入的位置。相比 704 找不到就直接返回 -1，这里需要更多考虑边缘临界的问题，比如 target 比所有 item 都小时 return 要怎么写…… 

> Q2: 为什么要 `return left`？
>
> - 这里可以考虑两个极端情况：
>   - target 过大时，left 在最后的循环中 `+1` 返回 left 即返回正确索引
>   - target 过小时，right 会在最后的循环中 `-1`，也许就是负数了，数组是不能有负数索引的，所以如果需要在数组中插入这个 target，只能放在 0 索引处，即 left 所在的位置









