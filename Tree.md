<!-- GFM-TOC -->
* [Recursive](#Recursive)
     * [1.TreeHeight](#1-TreeHeight)
<!-- GFM-TOC -->

# Recursive
## 1. TreeHeight
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
