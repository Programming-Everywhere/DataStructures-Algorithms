# Greedy - 贪心思想
1. [(455) Assign Cookies](https://leetcode.com/problems/assign-cookies/)
2. [435. Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/description/)
3. [452. Minimum Number of Arrows to Burst Balloons](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/description/)
4. [406. Queue Reconstruction by Height](https://leetcode.com/problems/queue-reconstruction-by-height/)
5. [121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/)
6. [122. Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/description/)
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
# 2 (435). Non-overlapping Intervals
[leetcode](https://leetcode.com/problems/non-overlapping-intervals/description/)
```java
class Solution {
    public int eraseOverlapIntervals(int[][] intervals) {
        /**
        1)核心思想： sort 这个array 
        2)然后三个ptr： preEnd， nextStart，nextEnd
        3)然后检查preEnd和nextStart的大小，只有 nextStart >=  preEnd， 我们就数数+1，然后preEnd 更新到nextEnd，这样依次类推
        4)最有用总长度 减去 数数,
        5)这个就是需要减去的结果。
        */
        if (intervals == null || intervals.length == 0) return 0;
        Arrays.sort(intervals, (a, b) -> a[1]-b[1]);
    
        int count = 1;
        int preEnd = intervals[0][1];
        for(int i = 1; i < intervals.length; i++) {
            int nextStart = intervals[i][0];
            int nextEnd = intervals[i][1];
            if(nextStart >= preEnd) { // no overlap
                preEnd = nextEnd;
                count++;
            }
        }
        return intervals.length - count;
    }
}
```
# 3. (452) Minimum Number of Arrows to Burst Balloons
[leetcode](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/description/)
```java
/**
核心思想：跟上题一样，sort y-axis，然后比较右和下个左，如果大 不管，如果小 就arrow++，因为不会沾到下个气球，并且把指标发在这个气球的右边，对比下一个。
*/
class Solution {
    public int findMinArrowShots(int[][] points) {
        /**[start,end]
           [10, 16], 
           [2,  8],
           [1,  6],
           [7,  12]]
           
           [
           [1,  6],
             [2,  8],
                 [7,  12]
                     [10, 16]]
           ]
        */
        if(points == null || points.length == 0) return 0;
        Arrays.sort(points, (a, b) -> a[1]- b[1]);
        
        int preEnd = points[0][1];
        int count = 1;
        for(int i = 1; i < points.length; i++) {
            
            int nextStart = points[i][0];
            if(preEnd < nextStart) {
                count++;
                preEnd = points[i][1];
            }
        }
        return count;
    }
}
```
# 4. (406) Queue Reconstruction by Height
[leetcode](https://leetcode.com/problems/queue-reconstruction-by-height/)
```java
/**
把身高的人放在最前面，这样一会插队（queue）先插他们，然后身高低的却是有同样 k 的可以插到 高的前方。（用index）
1. 身高按降序
2. 前方人数按升序。
*/
class Solution {
    public int[][] reconstructQueue(int[][] people) {
        if(people == null || people.length == 0) return new int[][]{};

        Arrays.sort(people, (a, b) -> (a[0] == b[0] ? a[1] - b[1]: b[0] - a[0]));
        // if h is equal, then k increasing order
        // if h is not equal, k decreasing order 

        List<int[]> queue = new ArrayList<>();
        for(int[] p: people) {
            queue.add(p[1], p);
        }      
        return queue.toArray(new int[queue.size()][]);
    }
}

/**

排好后：
7 0 
7 1 
6 1 
5 0 
5 2 
4 4 

index：
0 1 1 0 2 4 QUEUE

插完后：
5 0 
7 0 
5 2 
6 1 
4 4 
7 1 
*/
```
# 5. (121) Best Time to Buy and Sell Stock
[leetcode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/)
```java
class Solution {
    public int maxProfit(int[] prices) {
        if(prices == null || prices.length == 0) return 0;
        int min = prices[0];
        int profit = 0;
        for(int i = 1; i < prices.length; i++) {
            if(prices[i] < min) {
                min = prices[i];
            }
            profit = Math.max(profit,prices[i] - min);
        }
        return profit;
    }
}
```
# 6. (122) Best Time to Buy and Sell Stock II
[leetcode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/description/)
```java
// two pointers, and they always be together when checking it. 
class Solution {
    public int maxProfit(int[] prices) {
        int p1 = 0, p2 = 1;
        int profit = 0;
        while(p1 < prices.length && p2 < prices.length) {
            if(prices[p2] > prices[p1]) {
                profit += prices[p2] - prices[p1];
            }
            p1++;
            p2++;
        }
        return profit;
    }
}
```

