<!-- GFM-TOC -->
* [Recursive](#Recursive)
     * [1.TreeHeight](#1-TreeHeight)
     * [2.balanced-binary-tree](#2-balanced-binary-tree)
     * [3.DiameterBinaryTree](#3-DiameterBinaryTree)
     * [4.InvertBinaryTree](#4-InvertBinaryTree)
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
## 3. DiameterBinaryTree
[leetcode](https://leetcode.com/problems/diameter-of-binary-tree/description/)
```java
class Solution {
    int res = 0;
    public int diameterOfBinaryTree(TreeNode root) {
        /*
        1. find two length here: a, pass the root. b, don't pass the root
        2. compare these two length
        */
        int height = findHeight(root);
        return res;
    }
    private int findHeight(TreeNode root) {
        if(root == null) {
            return 0;
        }
        else {
            int L = findHeight(root.left);
            int R = findHeight(root.right);
            
            res = Math.max(res, L+R); // didn't pass the root
            return Math.max(L, R) + 1;
        }
    }
}
```
## 4. InvertBinaryTree
[leetcode](https://leetcode.com/problems/invert-binary-tree/description/)
```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if(root == null) return null;
        
        TreeNode temp = root.left;
        root.left = invertTree(root.right);
        root.right = invertTree(temp);
        return root;
        
    }
}
```
