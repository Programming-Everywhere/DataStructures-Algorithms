# Greedy - 贪心思想
1. [(455) Assign Cookies](https://leetcode.com/problems/assign-cookies/)

# 1. (455) Assign Cookies
[leetcode](https://leetcode.com/problems/assign-cookies/)
```java
class Solution {
    public int findContentChildren(int[] g, int[] s) {
        /**
        Assign cookie starting from the child with less greediness
        to gratify max number of kids/
        */
        Arrays.sort(g);
        Arrays.sort(s);
        int i = 0, j = 0;
        int count = 0;
        while(i < g.length && j < s.length) {
            if(g[i] <= s[j]) {
                count++;
                i++;
            }
            j++;
        }
        return count;
    }
}
```
