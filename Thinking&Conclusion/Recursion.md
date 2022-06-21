
### 对于递归的一些想法：

- 明确函数目标，设计签名函数
- 找到结束条件
- 找到等式关系：`f(x) = f(x.next) + <改变节点连接方向>`





- 206
- 21
- 509



>如果你实在找不出，你就先对 reverseList(head.next) 递归走一遍，看看结果是咋样的。
>
>也就是说，reverseList(head) 等价于 **reverseList(head.next)** + **改变一下1，2两个节点的指向**。
>
>——告别递归，连刷40道题，谈谈我的经验 - 帅地的文章 - 知乎 https://zhuanlan.zhihu.com/p/386785887

