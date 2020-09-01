1. [167. Two Sum II - Input array is sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/)
2. [633. Sum of Square Numbers](https://leetcode.com/problems/sum-of-square-numbers/description/)
3. [345. Reverse Vowels of a String](https://leetcode.com/problems/reverse-vowels-of-a-string/description/)
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
# 3. Reverse Vowels of a String
[leetcode](https://leetcode.com/problems/reverse-vowels-of-a-string/)
```java
/**
Write a function that takes a string as input and reverse only the vowels of a string.
Example 1:

Input: "hello"
Output: "holle"
*/
class Solution {
    public String reverseVowels(String s) {
        StringBuilder sb = new StringBuilder();
        char[] arr = s.toCharArray();
        int left = 0, right = s.length() - 1;
       
        while(left < right) {
            if(isVowel(arr[left]) && isVowel(arr[right])) {
                char temp = arr[left];
                arr[left] = arr[right];
                arr[right] = temp;  
                left++;
                right--;
            }
            else if(!isVowel(arr[left])) {
                left++;
            }
            else if(!isVowel(arr[right])) {
                right--;
            }
        }
        return sb.append(arr).toString();
    }
    private boolean isVowel(char c) {
        return c == 'a' || c == 'e' || c =='i' || c == 'o' || c == 'u' ||
            c == 'A' || c == 'E' || c =='I' || c == 'O' || c == 'U';
    }
}
```
