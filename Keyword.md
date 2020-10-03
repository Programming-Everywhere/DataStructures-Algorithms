# Keyword
- Binary tree and Binary Search Tree 
- Balanced BST]
- Full Binary Tree vs Complete Binary Tree vs Perfect BST
- Abstraction
- Interface
- Override
- Overloading

# 1. Binary tree and Binary Search Tree 
- Binary Tree: A tree whose elements have at most 2 children is called a binary tree
- Binary Search Tree: 
    1. The left subtree of a node contains only nodes with keys lesser than the node’s key.
    2. The right subtree of a node contains only nodes with keys greater than the node’s key.
    3. The left and right subtree each must also be a binary search tree.
# 2. Full Binary Tree vs Complete Binary Tree vs Perfect BST
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

# 3. Abstraction & Interface
- Abstraction: a process of hiding certain details, show only the essential detials. 
- Interface: it is one of two ways to achieve the abstraction. 

# 4. override vs overloading
- override: 
- overloading:
![overriding-vs-overloading-in-java](https://user-images.githubusercontent.com/19642027/94990186-1dc27700-0548-11eb-9951-468ee55920ed.png)

Use @Override Pro:
- Use it every time you override a method for two benefits. Do it so that you can take advantage of the compiler checking to make sure you actually are overriding a method when you think you are. This way, if you make a common mistake of misspelling a method name or not correctly matching the parameters, you will be warned that you method does not actually override as you think it does.
- Secondly, it makes your code easier to understand because it is more obvious when methods are overwritten.
