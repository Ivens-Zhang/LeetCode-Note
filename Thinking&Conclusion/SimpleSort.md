## 3 种简单排序

参考视频：https://www.bilibili.com/video/BV1b54y1Q7Pr?share_source=copy_web

相关题目：

- [215. Kth Largest Element in an Array](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/)

### 选择排序

选择排序原理就是从现有的集合中不断筛选出最大值、最小值，然后放入一个新的集合中。

```python
# 为 nums 排序
res = []
for i in range(0, len(nums)):
    val, idx = nums[0], 0
    for j in range(1, len(nums)):
        if nums[j] < val:
            val = nums[j]
            idx = j
    nums.pop(idx)
    res.append(val)

return res
```



### 冒泡排序

冒泡，更像一种**接力**。是先排好后面的元素，然后慢慢往前排。

> Q：为什么要在第二个循环中加入 i？
>
> A：因为从尾部起 i 个元素已经排好了，不需要和他们去比对了，提高效率。

```python
# 为 nums 排序
for i in range(0, len(nums) - 1):
    for j in range(0, len(nums) - 1 - i):
        if nums[j] > nums[j+1]:
            tmp = nums[j+1]
            nums[j+1] = nums[j]
            nums[j] = tmp
return nums
```



### 插入排序

从头遍历，将轮到的 item，放入索引前中对应的位置。

```python
# 为 nums 排序
for i in range(1, len(nums)):
    for j in range(0, i):
        if nums[i] < nums[j]:
            tmp = nums[i]
            nums.pop(i)
            nums.insert(j, tmp)
            break

return nums
```







