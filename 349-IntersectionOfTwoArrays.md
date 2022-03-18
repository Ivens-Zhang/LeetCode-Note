## [349. Intersection of Two Arrays](https://leetcode-cn.com/problems/intersection-of-two-arrays/)

#Array #BinarySearch

```tex
Given two integer arrays nums1 and nums2, return an array of their intersection. Each element in the result must be unique and you may return the result in any order.

 
Example 1:
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]

Example 2:
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [9,4]
Explanation: [4,9] is also accepted.
 

Constraints:
1 <= nums1.length, nums2.length <= 1000
0 <= nums1[i], nums2[i] <= 1000
```



Answer：

```py
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        result = []

        nums1, nums2 = list(set(nums1)), list(set(nums2))

        nums1.sort()
        nums2.sort()      

        for num1 in nums1:
            left, right = 0, len(nums2) - 1
            while left <= right:
                middle = (left + right) // 2
                if num1 == nums2[middle]:
                    result.append(num1)
                    break
                elif num1 > nums2[middle]:
                    left = middle + 1
                else:
                    right = middle - 1

        return result
```



Notes：

第一次我尝试使用最简单的双循环比对 intersection 项：

```py
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        result = []

        nums1, nums2 = list(set(nums1)), list(set(nums2))

        for num1 in nums1:
            for index2 in range(0, len(nums2)):
                if num1 == nums2[index2]:
                    result.append(num1)

        return result
```

但是时间复杂度为 $O(n^2)$，所以需要对算法进行优化；由于题目的标签中带有 “二分查找”，所以着重从这里思考：

1. 我们可以先对给定的两个数组进行排序+去重，数组排序的复杂度为 $O(log~n)$；

2. 然后循环数组一中元素（ $O(n)$），利用二分查找（复杂度为 $O(log~n)$）在数组二中找相同项，这时我们的时间复杂度为 $O(nlog~n)$。

经过优化，测试用例的执行用时也从平均 80+ms 降低到 40+ms：

![image-20220318004322344](https://gitee.com/zhangyi98/pictureBed/raw/master//img/image-20220318004322344.png)



一些想法：

- 如果涉及到有序、`int` 型数组，二分查找可以优先考虑使用
- 双循环基本是最差的解法了， $O(n^2)$的复杂度，使用其他算法基本都可以至少优化到$O(log~n)$

