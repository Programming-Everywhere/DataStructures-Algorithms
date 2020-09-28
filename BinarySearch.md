- [1 (69) Sqrt(x)](https://leetcode.com/problems/sqrtx/description/)
- [2  (744) Find Smallest Letter Greater Than Target](https://leetcode.com/problems/find-smallest-letter-greater-than-target/description/)

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
