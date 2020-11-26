<!-- GFM-TOC -->
* [Recursive](#Recursive)
     * [1.TreeHeight](#1-TreeHeight)
     * [2.balanced-binary-tree](#2-balanced-binary-tree)
     * [3.DiameterBinaryTree](#3-DiameterBinaryTree)
     * [4.InvertBinaryTree](#4-InvertBinaryTree)
* [LevelTraversal](#LevelTraversal)
     * [1.AverageofLevelsinBinaryTree](#1-AverageofLevelsinBinaryTree)
     * [2.FindBottomLeftTreeValue](#2-FindBottomLeftTreeValue)
* [OrderTraversal](#OrderTraversal)
     * [1. BinaryTreePreorderTraversal](#1-BinaryTreePreorderTraversal)
* [LCA](#LCA)
     * [1. LCA](#1-LCA)
* [BST](#BST)
     * [1.TrimaBST](#1-TrimaBST)
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
# LevelTraversal

## 1. AverageofLevelsinBinaryTree
[leetcode](https://leetcode.com/problems/average-of-levels-in-binary-tree/description/)
```java
lass Solution {
    public List<Double> averageOfLevels(TreeNode root) {
        List<Double> res = new ArrayList<>();
        Queue<TreeNode> queue = new LinkedList();
        queue.add(root);
        double sum = 0;
        while(!queue.isEmpty()) {
            int size = queue.size();
            for(int i = 0; i < size; i++) {
                TreeNode curr = queue.poll();
                sum += curr.val;
                if(curr.left != null) {
                    queue.add(curr.left);
                }
                if(curr.right != null) {
                    queue.add(curr.right);
                }
            }
            res.add(sum / size);
            sum = 0;
        }
        return res;
    }
}
```
## 2. FindBottomLeftTreeValue
```java
class Solution {
    public int findBottomLeftValue(TreeNode root) {
        if(root == null) return 0;
        TreeNode res = null;
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        while(!queue.isEmpty()) {
            int size = queue.size();
            res = queue.peek();
            for(int i = 0; i < size; i++) {
                TreeNode curr = queue.poll();
                if(curr.left != null) queue.add(curr.left);
                if(curr.right != null) queue.add(curr.right);
            }
        }
        return res.val;
    }
}
```
# OrderTraversal

## 1. BinaryTreePreorderTraversal
[leetcode](https://leetcode.com/problems/binary-tree-preorder-traversal/description/)
```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        //preorder: root -> left -> right
        List<Integer> res = new LinkedList<>();
        if(root == null) return res;
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        while(!stack.isEmpty()) {
            TreeNode curr = stack.pop();
            res.add(curr.val);
            if(curr.right != null) {
                stack.push(curr.right);
            }
            if(curr.left != null) {
                stack.push(curr.left);
            }
        }
        return res;
    }
}
```

# LCA
## 1. LCA
[leetcode](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root == null) return null;
        if(p == root || q == root) {
            return root;
        }
        TreeNode Left = lowestCommonAncestor(root.left, p, q);
        TreeNode Right = lowestCommonAncestor(root.right, p, q);
        
        if(Left != null && Right != null) {
            return root;
        }
        if(Left == null && Right != null) {
            System.out.println("right= " + Right.val);
            return Right;
        }
        if(Left != null && Right == null) {
            System.out.println("left= " + Left.val);
            return Left;
        }
        return null;
    }
}
```
# BST
## 1. TrimaBST 
[leetcode](https://leetcode.com/problems/trim-a-binary-search-tree/description/)
```java
public TreeNode trimBST(TreeNode root, int L, int R) {
    if (root == null) return null;
    if (root.val > R) return trimBST(root.left, L, R);
    if (root.val < L) return trimBST(root.right, L, R);
    root.left = trimBST(root.left, L, R);
    root.right = trimBST(root.right, L, R);
    return root;
}
```
