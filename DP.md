#### 递归和动态规划都是将原问题拆成多个子问题然后求解，他们之间最本质的区别是，动态规划保存了子问题的解，避免重复计算。
<!-- GFM-TOC -->
* [FibonacciSequence](#FibonacciSequence)
    * [1. StairsClimbing](#1-StairsClimbing)
    * [2. HouseRobber](#2-HouseRobber)
    * [3. HouseRobberII](#3-HouseRobberII)
    * [4. Find-the-Derangement-of-An-Array](#4-Find-the-Derangement-of-An-Array)

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
## 3. HouseRobberII
[leetcode](https://leetcode.com/problems/house-robber-ii/description/)
```java
class Solution {
    public int rob(int[] nums) {
        if(nums.length == 0) return 0;
        if(nums.length == 1) return nums[0];
        if(nums.length == 2) return Math.max(nums[0], nums[1]);
        int[] dp = new int[nums.length];
        dp[0] = nums[0];
        dp[1] = Math.max(nums[0], nums[1]);
        
        int[] dp2 = new int[nums.length];
        dp2[0] = 0;
        dp2[1] = nums[1];
        
        for(int i = 2; i < nums.length; i++) {
            dp[i] = Math.max(dp[i-1], dp[i-2] + nums[i]);
            dp2[i] = Math.max(dp2[i-1], dp2[i-2] + nums[i]);
        }
        
       
        return Math.max(dp[nums.length - 2], dp2[nums.length - 1]);
    }
}
//[7,4,1,9,3,8,6]
```
## 4. Find-the-Derangement-of-An-Array
[leetcode](https://leetcode.com/problems/find-the-derangement-of-an-array/)
```java
class Solution {
    public int findDerangement(int n) {
        // 1, 2, 3, 4, ...n
        // _, 2, 3, 1, ...n
        /*1: now 4 can be in 1st position, then we need to find postions for rest of n-2 nums.
          2: 4 not in 1st place but other place, then we need to find pos for rest of n-1(except 1)
        */
        
        if(n == 0) return 1;
        if(n == 1) return 0;
        long[] dp = new long[n + 1];
        dp[0] = 1;
        dp[1] = 0;
        for(int i = 2; i <= n; i++) {
            dp[i] = (i - 1) * (dp[i - 1] + dp[i - 2]) %1000000007;    
        }
       return (int)dp[n];
    }
}
```
