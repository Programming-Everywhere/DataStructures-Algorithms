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
