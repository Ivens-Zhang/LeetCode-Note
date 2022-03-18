## [1287. Element Appearing More Than 25% In Sorted Array](https://leetcode-cn.com/problems/element-appearing-more-than-25-in-sorted-array/)

#Array #BinarySearch

```te
Given an integer array sorted in non-decreasing order, there is exactly one integer in the array that occurs more than 25% of the time, return that integer.

Example 1:
Input: arr = [1,2,2,6,6,6,6,7,10]
Output: 6

Example 2:
Input: arr = [1,1]
Output: 1
 
Constraints:
1 <= arr.length <= 104
0 <= arr[i] <= 105
```



Answer：

```python
class Solution:
    def findSpecialInteger(self, arr: List[int]) -> int:
        span = len(arr) // 4

        for i in range(0, len(arr) - span):
            if arr[i] == arr[i + span]:
                return arr[i]
```



Notes：

这题直接使用双循环即可，但是复杂度为 $O(n^2)$ 有点太慢，通过题目描述可知，有且只有一个数出现的频率超过 25%；所以，由此可推出，在整个数组中，一定有一个片段，长度超过数组长度的 25%，且该片段内全为同一个数。推理过程可参考以下视频中的第三种解法：[【LeetCode解题】1287.有序数组里出现次数超过1/4的元素](https://www.bilibili.com/video/BV1VJ411t7hj?spm_id_from=333.337.search-card.all.click)。

> Q1：如何确定这个片段长度？
>
> - 举几个临界值，可以得出 span 为数组长度除 4 并向下取整

> Q2：应该比较哪两个数？
>
> - arr[i] 和 arr[i + span]