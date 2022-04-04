## [344. Reverse String](https://leetcode-cn.com/problems/reverse-string/)

#Array #TwoPointers

Write a function that reverses a string. The input string is given as an array of characters `s`.

You must do this by modifying the input array [in-place](https://en.wikipedia.org/wiki/In-place_algorithm) with `O(1)` extra memory.

**Example 1:**

```
Input: s = ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]
```

**Example 2:**

```
Input: s = ["H","a","n","n","a","h"]
Output: ["h","a","n","n","a","H"]
```

 

Answer:

本题思路很简单，利用双指针，左右设置一个指针对换元素即可。

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """

        # 双指针，比递归更适合这道题
        l, r = 0, len(s) - 1

        while l < r:
            s[l], s[r] = s[r], s[l]
            l, r = l+1, r-1

        return s
```

这题目的关键点在 `in-place` 我们在整理数组的时候需要非常注意有没有改变数组的内存地址，如果改变了是无法提交通过的。