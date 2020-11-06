<!-- GFM-TOC -->
* [Recursive](#Recursive)
     * [1.TreeHeight](#1-TreeHeight)
     * [2.balanced-binary-tree](#2-balanced-binary-tree)
<!-- GFM-TOC -->

# Recursive
## 1. TreeHeight
```java
class Solution {
    public int maxDepth(TreeNode root) {
        if(root == null) return 0;
        else {
            return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
        }
    }
}
```
## 2. balanced-binary-tree
[leetcode](https://leetcode.com/problems/balanced-binary-tree/description/)
```java
class Solution {
    public boolean isBalanced(TreeNode root) {
        return height(root) != -2;
    }
    private int height(TreeNode root) {
        if(root == null) {
            return 0;
        }
        int leftHeight = height(root.left);
        int rightHeight = height(root.right);
        if(leftHeight == -2 || rightHeight == -2 || Math.abs(leftHeight - rightHeight) > 1) {
            return -2;
        }
        return Math.max(leftHeight, rightHeight) + 1;
    }
}
```
