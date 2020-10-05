-[1. (241) Different Ways to Add Parentheses](https://leetcode.com/problems/different-ways-to-add-parentheses/description/)


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
