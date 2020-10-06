- [1. (241) Different Ways to Add Parentheses](https://leetcode.com/problems/different-ways-to-add-parentheses/description/)
- [2. (95) Unique Binary Search Trees II](https://leetcode.com/problems/unique-binary-search-trees-ii/description/)


# 1.(241) Different Ways to Add Parenthese
[leetcode](https://leetcode.com/problems/different-ways-to-add-parentheses/description/)
```java
class Solution {
    public List<Integer> diffWaysToCompute(String input) {
        
        // once we find the operator, we will split to two parts based on the index of perator, then we will recusively call the fuction then to the result of that part.
        List<Integer> res = new ArrayList<>();
        for(int i = 0; i < input.length(); i++) {
            char c = input.charAt(i);
            if(c == '+' || c == '-' || c =='*') {
                List<Integer> left = diffWaysToCompute(input.substring(0, i));
                List<Integer> right = diffWaysToCompute(input.substring(i + 1));
                for(int l: left) {
                    for(int r: right) {
                        if(c == '+') {
                            res.add(l + r);
                        }
                        if(c == '-') {
                            res.add(l - r);
                        }
                        if(c == '*') {
                            res.add(l * r);
                        }
                    }
                }
            }
        }
        if(res.size() == 0) {
            res.add(Integer.valueOf(input));
        }
        return res;
    }
}
        
        /**(1)
        2-1-1+1
         /  \
       2 -  (1-1+1)
      /       \
     2    -  1 - (1+1)
    /       /  -   /\
   2    -  1   -  1 + 1  
                   \/
           1    -   2
               \/
     2   -     -1
         \/
         3
         (2)
        2-1-1+1  
        /     \
    (2-1) - (1+1) 
     1    -  2 = -1
         (3)        
        2-1-1+1  
        /     \
     (2-1-1) + 1
      / \
     2 - (1-1) + 1
     2 -0+1 = 3 
     
       -->  (3.1) 
       2-1-1+1  
        /     \
     (2-1-1) + 1
      /   \
 (2 -1)  - (1) + 1
    1-1        +1  = 1 
        */ 
```
# 2. (95) Unique Binary Search Trees II
[leetcode](https://leetcode.com/problems/unique-binary-search-trees-ii/description/)
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<TreeNode> generateTrees(int n) {
        // 1, 2, 3, 4,,,n 
        // node is i, left: 1~i, right i+1...n 
        if(n == 0) return new LinkedList<TreeNode>();
        return generateSubtree(1, n);
    }
    private List<TreeNode> generateSubtree(int start, int end) {
        List<TreeNode> allTrees = new LinkedList<>();
        if(start > end) {
            allTrees.add(null);
            return allTrees;
        }
        for(int i = start; i <= end; i++) {
            List<TreeNode> leftTree = generateSubtree(start, i - 1);
            List<TreeNode> rightTree = generateSubtree(i+1, end);
            
            for(TreeNode left: leftTree) {
                for(TreeNode right: rightTree) {
                    TreeNode root = new TreeNode(i);
                    root.left = left;
                    root.right = right;
                    
                    allTrees.add(root);
                }
            }
        }
        return allTrees;
        
    }
}
```

