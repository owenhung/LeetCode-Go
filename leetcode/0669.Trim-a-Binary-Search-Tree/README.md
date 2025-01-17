# [669. Trim a Binary Search Tree](https://leetcode.com/problems/trim-a-binary-search-tree/)


## 题目

Given the `root` of a binary search tree and the lowest and highest boundaries as `low` and `high`, trim the tree so that all its elements lies in `[low, high]`. Trimming the tree should **not** change the relative structure of the elements that will remain in the tree (i.e., any node's descendant should remain a descendant). It can be proven that there is a **unique answer**.

Return *the root of the trimmed binary search tree*. Note that the root may change depending on the given bounds.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/09/09/trim1.jpg](https://assets.leetcode.com/uploads/2020/09/09/trim1.jpg)

```
Input: root = [1,0,2], low = 1, high = 2
Output: [1,null,2]
```

**Example 2:**

![https://assets.leetcode.com/uploads/2020/09/09/trim2.jpg](https://assets.leetcode.com/uploads/2020/09/09/trim2.jpg)

```
Input: root = [3,0,4,null,2,null,null,1], low = 1, high = 3
Output: [3,2,null,1]
```

**Example 3:**

```
Input: root = [1], low = 1, high = 2
Output: [1]
```

**Example 4:**

```
Input: root = [1,null,2], low = 1, high = 3
Output: [1,null,2]
```

**Example 5:**

```
Input: root = [1,null,2], low = 2, high = 4
Output: [2]
```

**Constraints:**

- The number of nodes in the tree in the range `[1, 10^4]`.
- `0 <= Node.val <= 10^4`
- The value of each node in the tree is **unique**.
- `root` is guaranteed to be a valid binary search tree.
- `0 <= low <= high <= 10^4`

## 题目大意

给你二叉搜索树的根节点 root ，同时给定最小边界low 和最大边界 high。通过修剪二叉搜索树，使得所有节点的值在[low, high]中。修剪树不应该改变保留在树中的元素的相对结构（即，如果没有被移除，原有的父代子代关系都应当保留）。 可以证明，存在唯一的答案。所以结果应当返回修剪好的二叉搜索树的新的根节点。注意，根节点可能会根据给定的边界发生改变。

## 解题思路

- 这一题考察二叉搜索树中的递归遍历。递归遍历二叉搜索树每个结点，根据有序性，当前结点如果比 high 大，那么当前结点的右子树全部修剪掉，再递归修剪左子树；当前结点如果比 low 小，那么当前结点的左子树全部修剪掉，再递归修剪右子树。处理完越界的情况，剩下的情况都在区间内，分别递归修剪左子树和右子树即可。

## 代码

```go
package leetcode

import (
	"github.com/halfrost/leetcode-go/structures"
)

// TreeNode define
type TreeNode = structures.TreeNode

/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */

func trimBST(root *TreeNode, low int, high int) *TreeNode {
	if root == nil {
		return root
	}
	if root.Val > high {
		return trimBST(root.Left, low, high)
	}
	if root.Val < low {
		return trimBST(root.Right, low, high)
	}
	root.Left = trimBST(root.Left, low, high)
	root.Right = trimBST(root.Right, low, high)
	return root
}
```