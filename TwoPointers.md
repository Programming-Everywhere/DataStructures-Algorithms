1. [167. Two Sum II - Input array is sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/)
2. [633. Sum of Square Numbers](https://leetcode.com/problems/sum-of-square-numbers/description/)
3. 
# 1.Two Sum II - Input array is sorted
```java
/** since it is sorted, we can use two pointers from left and right.
1. if it is bigger than target, means, our right side is too big, right--
2. if it is smaller than target, means our left side is too small, left++
3. find it..
*/
class Solution {
   public int[] findTarget(int[] nums, int target){ 
      int left = 0, right = nums.length - 1;
      int[] res = new int[2];
      while(left < right) {
         if(nums[left] + nums[right] == target) {
             res[0] = left;
             res[1] = right;
         }
         else if(nums[left] + nums[right] < target) {
             right--;
         }
         else {
             left++;
         }
      } 
      return res;
   }
}
```
# 2. Sum of Square Numbers
```java
/**
1. two pointers
2. the second one can be sqrt(c), because we will have ptr2*ptr2
*/ 
class Solution {
   public boolean judgeSquareSum(int c) {
      int p1 = 0, p2 = (int)Math.sqrt(c);
      while(p1 <= p2) {
         int sum = p1*p1 + p2*p2;
         if(sum == c) return true;
         else if(sum > c) p2--;
         else p1++;
      }
      return false;
   }
}

```
