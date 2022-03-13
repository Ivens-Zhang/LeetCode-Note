## 704. Binary Search

Label：#Array #BinarySearch

```te
Given an array of integers nums which is sorted in ascending order, and an integer target, write a function to search target in nums. If target exists, then return its index. Otherwise, return -1.

You must write an algorithm with O(log n) runtime complexity.
 

Example 1:

Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4
Example 2:

Input: nums = [-1,0,3,5,9,12], target = 2
Output: -1
Explanation: 2 does not exist in nums so return -1
 

Constraints:

1 <= nums.length <= 104
-104 < nums[i], target < 104
All the integers in nums are unique.
nums is sorted in ascending order.

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/binary-search
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```



Answer:

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left ,right = 0, len(nums) - 1

        while left <= right:
            middle = (left + right) // 2
            if nums[middle] == target:
                return middle
            elif nums[middle] < target:
                left = middle + 1
            else:
                right = middle - 1
        return -1
```



Notes:

> Q1: 为什么使用二分查找？
>
> - 因为题目要求所使用的算法时间复杂度须为 logn，所以自然排除遍历搜索



> Q2: 如何设置 `middle` 索引？
>
> - 使用 python 的 `//` 运算符，相当于 `JavaScript` 中的 `floor`



> Q3: 给循环设置什么跳出条件？
>
> - left > right 即可，有很多种选择，这种最简单易于理解



> Q4: 按照什么规则更新 left 和 right 的值？为什么不直接 `left = middle` ?
>
> - 如果直接 `left = middle` 这样写会导致范围无法变化，注意这里用的是`//` 运算符，如果出现 `left ,right = 0, 1` 的情况，那 `middle ` 会一直都是 0。而且，`middle` 对应的值肯定不在 `target` 所在的范围，因为如果匹配直接就返回了；例如：`nums = [-1,0,3,5,9,12], target = 9`，我们在第一次的二分查找中发现 `nums[middle] = 3`， target 的值要大于这个中间点，所以我们在下一次设置区间时，应该直接取比当前中间点再大一个的索引。





