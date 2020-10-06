- [1 (69) Sqrt(x)](https://leetcode.com/problems/sqrtx/description/)
- [2  (744) Find Smallest Letter Greater Than Target](https://leetcode.com/problems/find-smallest-letter-greater-than-target/description/)
- [3 (540) Single Element in a Sorted Array](https://leetcode.com/problems/single-element-in-a-sorted-array/description/)
- [4. (278) First Bad Version](https://leetcode.com/problems/first-bad-version/)
- [5. (153) Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/submissions/)
- [6. (34) Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)


# 1 (69) Sqrt(x)
[leetcode](https://leetcode.com/problems/sqrtx/description/)
```java
class Solution {
    public int mySqrt(int x) {
       /**
       8 
          4 
       1 2 3 4
         2 * 2 = 4
         left right mid, -> mid * mid = x return mid
         mid * mid > x -> mid > x / mid -> right = mid - 1
         mid < x / mid -> left = mid + 1
         
         3 
         1 2 3
         left right mid sqrt
         1     3    2    3/2=1
         3     3    3    3/3=1
         3+1=4
         
       */
        int left = 1, right = x;
        while(left <= right) {
            int mid = left + (right - left)/2;
            int sqrt = x / mid;
            if(sqrt == mid) {
                return mid;
            }
            else if(sqrt < mid) {
                right = mid - 1;
            }
            else {
                left = mid + 1;
            }
        }
        return right;
    }
}
```

# 2  (744) Find Smallest Letter Greater Than Target
[Leetcode](https://leetcode.com/problems/find-smallest-letter-greater-than-target/description/)
```java
class Solution {
    public char nextGreatestLetter(char[] letters, char target) {
        /*
find smallest but larger than target 
1. if it is equal, we check the right part by left = mid + 1;
2. if it is smaller than target, we check the right part by left = mid + 1;
3. if it is larger(satisfied question), we will save this one for now. (Because we will see if we still can go left, which will be smaller then we saved, but larger than target)
        */
        char res = letters[0];
        int left = 0, right = letters.length - 1;
        while(left <= right) {
            int mid = left + (right - left) / 2;
            if(letters[mid] == target) {
                left = mid + 1;
            }
            else if(letters[mid] < target) {
                left = mid + 1;
            }
            else {
                // this will make sure we find the 1st larger one. 
                res = letters[mid];
                right = mid - 1;
            }
        }
        return res;
    }
}
```
# 3. (540) Single Element in a Sorted Array
[leetcode](https://leetcode.com/problems/single-element-in-a-sorted-array/description/)
```java
class Solution {
    public int singleNonDuplicate(int[] nums) {
        int low = 0, high = nums.length - 1;
        while(low < high) {
            int mid = low + (high - low) / 2;
            if(mid % 2 == 1) {
                mid--;
            }
            if(nums[mid] == nums[mid + 1]) {
                low = mid + 2;
            }
            else {
                high = mid;
            }
        }
        return nums[low];
    }
}
```
# 4. (278) First Bad Version
[leetcode](https://leetcode.com/problems/first-bad-version/)
```java
public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        /**
        1 2 3 4 5
        f f t t t
        */
        int low = 0, high = n - 1;
        while(low <= high) {
            int mid = low + (high - low)/2;
            if(!isBadVersion(mid) && isBadVersion(mid + 1)) {
                return mid+1;
            }
            else if(isBadVersion(mid)) {
                high = mid - 1;
            }
            else if(!isBadVersion(mid) && !isBadVersion(mid + 1)) {
                low = mid + 1;
            }
        }
        return low;
    }
}
```
# 5.(153) Find Minimum in Rotated Sorted Array
[leetcode](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/submissions/)
```java
class Solution {
  public int findMin(int[] nums) {
     // 5,6,0,1,2,3,4
     int left = 0, right = nums.length - 1;
     while(left < right) {
        int mid = left + (right - left) / 2;
        if(mid >= 1 &&nums[mid] < nums[mid-1]) {
            return nums[mid];
        } 
        else if(nums[mid] < nums[right]){ 
             right = mid - 1;
        }
        else {
             left = mid + 1;
        }
     }
     return nums[left];
  
  }
}
```
# 6. (34) Find First and Last Position of Element in Sorted Array
[leetcode](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)
```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
          // [5,7,7,8,8,10]  t = 8
         
          int[] res = {-1, -1};
          if(nums.length == 0 || nums == null) return res;
          res[0] = findLeft(nums,target);
          res[1] = findRight(nums, target);
          return res;
    }
    private int findLeft(int[] nums, int target) {
        int low = 0, high = nums.length - 1;
        int startPoint = -1;
        while(low <= high) {
           int mid = low + (high - low) / 2;
           if(nums[mid] == target) {
              // find mid's left still is the target
              startPoint = mid;
              high = mid - 1;
           }
           else if(nums[mid] < target) {
              low = mid + 1;
           }
           else {
             high = mid - 1;
           }
        }
        return startPoint;
    }
    private int findRight(int[] nums, int target) {
        int low = 0, high = nums.length - 1;
        int endPoint = -1;
        while(low <= high) {
           int mid = low + (high - low) / 2;
           if(nums[mid] == target) {
              // find mid's left still is the target
              endPoint = mid;
              low = mid + 1;
           }
           else if(nums[mid] < target) {
              low = mid + 1;
           }
           else {
             high = mid - 1;
           }
        }
        return endPoint;
    }
}
```
# 7. Binary Searchable Elements (Google onsite Oct 2020)
```html
Binary search is a search algorithm usually used on a sorted sequence to quickly find an element with a given value. 
In this problem we will evaluate how binary search performs on data that isn't necessarily sorted. 
An element is said to be binary searchable if an element can be found provided the pivot is chosen everytime as the 
middle element - like in a regular binary search.
We need to find total number of elements which are binary searchable.

Example 1:
[2, 1, 3, 4, 6, 5] 
Output: 4
Explanation: 3 is searchable, 2 is searchable, 1 not searchable, 6 is searchable, 4 is seachable, 5 is not searchable 


Example 2:
Input: [1, 3, 2]
Output: 2
Explanation: 3 and 1 are searchable - you look for 3 - find it in the middle, look for 1 - you search the left half....search for 2, 
you look for it in the left half but didn't find.
```
```java
// pretend the array is a binary search tree, DFS/BFS all pivot elements and keep track the lower and upper bound for the left and right children
class Solution {
   int count = 0;
   public int BS(int[] arr) {
       checkTree(arr, Integer.MIN_VALUE, Integer.MAX_VALUE, 0, arr.length - 1);
       return count;
   }
   private void checkTree(int[] arr, int min, int max, int low, int high) {
      if(low > high) return;
      int mid = low + (high - low) / 2;
      if(arr[mid] > min && arr[mid] < max) {
         count++;
      }
      checkTree(arr, min, arr[mid], low, mid - 1);
      checkTree(arr, arr[mid], max, mid + 1, high);
   }
}
```
