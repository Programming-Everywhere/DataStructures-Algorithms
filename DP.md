#### 递归和动态规划都是将原问题拆成多个子问题然后求解，他们之间最本质的区别是，动态规划保存了子问题的解，避免重复计算。
<!-- GFM-TOC -->
* [FibonacciSequence](#FibonacciSequence)
    * [1. StairsClimbing](#1-StairsClimbing)
    * [2. HouseRobber](#1-HouseRobber)

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
## 2. HouseRobber
[leetcode](https://leetcode.com/problems/house-robber/description/)
```java
public Solution {
  
   public int rob(int[] nums) {
     if(nums.length == 0) return 0;
     if(nums.length == 1) return nums[0];
     if(nums.length == 2) return Math.max(nums[0], nums[1]);
     int[] dp = new int[nums.length];
     dp[0] = nums[0];
     dp[1] = nums[1];
     for(int i =2; i < nums.length; i++) {
        dp[i] = Math.max(dp[i-1], dp[i-2] + nums[i]);
     }
     return dp[nums.length - 1];
   }

}

```
