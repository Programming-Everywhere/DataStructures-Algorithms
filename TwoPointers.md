```html
Two pointers scinarios: 
1. left_pointer and right_pointer, iterate towards the middle
2. ptr1 = 0, ptr2 = Math.sqrt(num)
3. walke = head, runner = head
4. ptr1 = 0, ptr2 = 0
```


1. [167. Two Sum II - Input array is sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/)
2. [633. Sum of Square Numbers](https://leetcode.com/problems/sum-of-square-numbers/description/)
3. [345. Reverse Vowels of a String](https://leetcode.com/problems/reverse-vowels-of-a-string/description/)
4. [680. Valid Palindrome II](https://leetcode.com/problems/valid-palindrome-ii/)
5. [88. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/)
6. [141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/description/)
7. [524. Longest Word in Dictionary through Deleting](https://leetcode.com/problems/longest-word-in-dictionary-through-deleting/description/)
# 1.Two Sum II - Input array is sorted
[leetcode](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/)
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
[leetcode](https://leetcode.com/problems/sum-of-square-numbers/description/)
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
# 4. Valid Palindrome II
```java
/**
helper()
*/
class Solution {
    public boolean validPalindrome(String s) {
        int left = 0, right = s.length() - 1;
        
        while(left < right) {
            if(s.charAt(left) == s.charAt(right)) {
                left++;
                right--;
            }
            else {
                return helper(s, left + 1, right) || helper(s, left, right - 1);   
            }
        }
        return true;
    }
    private boolean helper(String s, int left, int right) {
        while(left < right) {
            
            if(s.charAt(left) != s.charAt(right)) {
                return false;
            }
            
            left++;
            right--;
        }
        return true;
    }
}
```
# 5. 88. Merge Sorted Array
[leetcode](https://leetcode.com/problems/merge-sorted-array/)
```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int ptr1 = m-1, ptr2 = n-1;
        int j = m+n-1;
        while(ptr1 >= 0 && ptr2 >= 0 ) {
            if(nums1[ptr1] > nums2[ptr2]) {
                nums1[j] = nums1[ptr1];
                ptr1--;
                j--;
            }
            else {
                nums1[j] = nums2[ptr2];
                ptr2--;
                j--;
            }
        }
        while(ptr2 >= 0) {
            nums1[j] = nums2[ptr2];
            ptr2--;
            j--;
        }}}
  ```
# 6. Linked List Cycle
[leetcode](https://leetcode.com/problems/linked-list-cycle/description/)
```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        if(head == null) return false;
        ListNode runner = head;
        ListNode walker = head;
        while(runner.next != null && runner.next.next != null) {
            runner = runner.next.next;
            walker = walker.next;
            if(walker == runner) {
                return true;
            }
        }
        return false;
    }
}
```
# 7. Longest Word in Dictionary through Deleting
[leetcode](https://leetcode.com/problems/longest-word-in-dictionary-through-deleting/description/)
```java
class Solution {
    public String findLongestWord(String s, List<String> d) {
        
        String longest = "";
        for(String target: d) {
            int l1 = longest.length(), l2 = target.length();
            if(l1 > l2 || (l1 == l2 && longest.compareTo(target) < 0)) {
                continue;
            }
            if(helper(s, target)) {
                longest = target;
            }
        }
        return longest; 
    }
    
    private boolean helper(String source, String target) {
            int p1 = 0, p2 = 0;
            while(p1 < source.length() && p2 < target.length()) {
                if(source.charAt(p1) == target.charAt(p2)) {
                    p1++;
                    p2++;
                }
                else {
                    p1++;
                }
            }
            return p2 == target.length();
    }
}

```
