# 动态规划

## 基本概念

把原问题分解为相对简单的子问题的方式求复杂问题的方法。适用于又重叠子问题和最有子结构性质的问题，消耗时间相对较少。主要实现方式是，先计算子问题，然后存储结果，再利用存储的结果来解后续问题，直到原问题被解决为止。动态规划需要解决的问题主要具有两种特性：最佳化结构以及重叠自问题。如果是不重叠的子结构，那就成了分治。

最佳化结构说明问题的解可以由子结构的最优解来得出，这种结构一般由递归形式说明。

重叠子结构说明子结构可能会被重复计算。

动态规划的实现有两种：

1. 自顶向下
2. 自底向上

### 自顶向下

自顶向下的解法就相当于递归的形式，如果问题的解可以用子问题的解以递归的形式来求出，并且自问题存在重叠，那就可以直接存储自问题的解。之后每次解一个问题的时候都先查看是否已经有解，如果有了就直接取出来，没有再计算并存储新的结果。

### 自底向上

如果能够用递归的形式来表述一个问题，就可以重新组合公式获得自底向上的犯法。先尝试解决某个自问题，然后用其解去解决更上一层的问题。

### 重要概念

最优子结构，边界，状态转移公式

## 题目

### [10. Regular Expression Matching](./Code/2018-5-22/RegularExpression.md)

这题非常难看出来方程，在匹配的时候需要换个方向去想。判断s和p是否匹配的时候，其实就两种情况，一种是第一个字符不匹配，直接return False。另一种是第一个字符匹配，然后看s-1和p-1是不是匹配。这样的话其实就有点DP的样子了，然后就是构建方程。因为这道题中的\*可以匹配的非常多，所以方程其实很难构建。个人觉得，类似这种题目只能通过不断练习来积累。

### [62. Unique Paths](./Code/2018-6-6/UniquePath.md)

这题是非常标准的DP，方程和子结构都很好看出来。

### [70. Climbing Stairs](./Code/2018-6-6/ClimbingStairs.md)

要注意n为1的情况