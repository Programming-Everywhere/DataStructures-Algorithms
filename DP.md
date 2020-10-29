#### 递归和动态规划都是将原问题拆成多个子问题然后求解，他们之间最本质的区别是，动态规划保存了子问题的解，避免重复计算。
<!-- GFM-TOC -->
* [FibonacciSequence](#FibonacciSequence)
    * [1. StairsClimbing](#1-StairsClimbing)
    * [2. HouseRobber](#2-HouseRobber)
    * [3. HouseRobberII](#3-HouseRobberII)
    * [4. Find-the-Derangement-of-An-Array](#4-Find-the-Derangement-of-An-Array)
    * [5. Cow-production](#5-Cow-production)
* [MatrixPath](#MatrixPath)
    * [1. Minimum-Path-Sum](#1-Minimum-Path-Sum)



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
## 5. Cow-production
```html
假设农场中成熟的母牛每年都会生 1 头小母牛，并且永远不会死。
第一年有 1 只小母牛，从第二年开始，母牛开始生小母牛。
每只小母牛 3 年之后成熟又可以生小母牛。给定整数 N，求 N 年后牛的数量。
```
```java
class Solution {
   public int cows(int years) {
      if (year == 0) return 0;
      if (year == 1) return 1;
      if (year == 2) return 2;
      int[] dp = new int[years+1];
      dp[0] = 0;
      dp[1] = 1;
      dp[2] = 2;
      for(int i = 3; i <= years; i++) {
         dp[i] = dp[i - 1] + dp[i - 2];
      }
      return dp[year];
   }
 
}
```
# MatrixPath

## 1. Minimum-Path-Sum
[leetcode](https://leetcode.com/problems/minimum-path-sum/description/)
```java
class Solution {
    public int minPathSum(int[][] grid) {
       /* bottom up!  
       1. build a dp[][] to memorize the sum
       2. then backward to fill dp[][].
       3. dp[i][j] can have min(dp[i+1][j], dp[i][j+1]);
       4. finnally return dp[0][0]
       */
        int m = grid.length, n = grid[0].length;
        int[][] dp = new int[grid.length][grid[0].length];
        for(int i = grid.length - 1; i >= 0; i--) {
            for(int j = grid[0].length - 1; j >= 0; j--) {
                if(i == m-1 && j != n - 1){
                    dp[i][j] = grid[i][j] + dp[i][j+1];
                }
                else if(i != m-1 && j == n - 1){
                    dp[i][j] = grid[i][j] + dp[i+1][j];
                }
                else if(i != m-1 && j != n - 1){
                     dp[i][j] = grid[i][j] + Math.min(dp[i+1][j], dp[i][j+1]); 
                }
                else {
                    dp[i][j] = grid[i][j];
                }
            }
        }
        return dp[0][0];
    }
}
```

