#### 递归和动态规划都是将原问题拆成多个子问题然后求解，他们之间最本质的区别是，动态规划保存了子问题的解，避免重复计算。
<!-- GFM-TOC -->
* [FibonacciSequence](#FibonacciSequence)
    * [1. StairsClimbing](#1-StairsClimbing)

<!-- GFM-TOC -->

# FibonacciSequence

## 1. StairsClimbing
[leetcode](https://leetcode.com/problems/climbing-stairs/)
```java
class Solution {
    public int climbStairs(int n) {
        if(n <= 2) return n;
        int[] mem = new int[n + 1];
        mem[1] = 1;
        mem[2] = 2;
        for(int i = 3; i <= n; i++) {
            mem[i] = mem[i-1] + mem[i - 2];
        }
        return mem[n];
    }
}
```
