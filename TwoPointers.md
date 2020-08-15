1. [167. Two Sum II - Input array is sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/)
2. 
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
