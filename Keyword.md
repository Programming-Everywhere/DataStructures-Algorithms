# Keyword
- 1. Binary tree and Binary Search Tree 
- 2. Balanced BST
- 3. Full Binary Tree vs Complete Binary Tree vs Perfect BST
- 4. Abstraction
- 5. Interface
- 6. Override
- 7. Overloading

# 1. Binary tree and Binary Search Tree 
- Binary Tree: A tree whose elements have at most 2 children is called a binary tree
- Binary Search Tree: 
    1. The left subtree of a node contains only nodes with keys lesser than the node’s key.
    2. The right subtree of a node contains only nodes with keys greater than the node’s key.
    3. The left and right subtree each must also be a binary search tree.

```html
Full Binary Tree: A Binary Tree is full if every node has 0 or 2 children. Following are examples of a full binary tree.

         18
       /    \   
     15      20    
    /  \       
   40   50   
  /  \
 30  50

Complete Binary Tree: A Binary Tree is complete Binary Tree if all levels are completely filled except possibly the last level and the last level has all keys as left as possible.

            18
       /         \  
     15           30  
    /  \         /  \
  40    50     100   40
 /  \   /
8   7  9 

Perfect Binary Tree: A Binary tree is Perfect Binary Tree in which all internal nodes have two children and all leaves are at same level.

           18
       /       \  
     15         30  
    /  \        /  \
  40    50    100   40
```
