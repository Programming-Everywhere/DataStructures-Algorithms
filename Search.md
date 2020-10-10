### DFS
- [1. (1239) Maximum Length of a Concatenated String with Unique Characters](https://leetcode.com/problems/maximum-length-of-a-concatenated-string-with-unique-characters/)

### BFS 
- [1.(1091) Shortest Path in Binary Matrix](https://leetcode.com/problems/shortest-path-in-binary-matrix/)
- [2.(279) Perfect Squares](https://leetcode.com/problems/perfect-squares/)
- [3.(127) Word Ladder](https://leetcode.com/problems/word-ladder/)

# BFS (Breadth first search)
 - 广度优先搜索一层一层的进行遍历。
 - 每层遍历都是以上一层遍历的结果作为起点。
 - 遍历一个距离能访问的所有节点
 - 访问过的节点不能再次被遍历
![Untitled (Draft)-1](https://user-images.githubusercontent.com/19642027/95317898-cc75f880-0863-11eb-99de-afc62407a41b.jpg)
 -  第一层：0 -> 5,1,2,6
 -  第二层：5->（3，4）。。。6->（4）。。。2->（）。。。1->（）
 -  第三层：3->()....4->()
 
 - 比如每个节点的距离相同，那样先遍历的节点i和后遍历的节点j，就有di <= dj, 这样我们可以求最短路径。
 - 在用BFS时候，我们要用：queue：存储每一轮遍历得到的节点  visited【】：标记已经访问过
 ## 1. (1091) Shortest Path in Binary Matrix(Medium)
 [leetcode](https://leetcode.com/problems/shortest-path-in-binary-matrix/)
 ```java
 class Solution {
    int[][] directions = {{0,1},{0,-1},{1,0},{1,1},{1,-1},{-1,0},{-1,1},{-1,-1}};
    public int shortestPathBinaryMatrix(int[][] grid) {
        //BFS
        int m = grid.length;
        int n = grid[0].length;
        if(grid[0][0] == 1 || grid[m - 1][n - 1] == 1) {
            return -1;
        }
        boolean[][] visited = new boolean[m][n];
        Queue<int[]> queue = new LinkedList<>();
        
        queue.add(new int[]{0, 0});
        visited[0][0] = true;
        int count = 0;
        
        while(!queue.isEmpty()) {
            int size = queue.size();
            for(int i = 0; i < size; i++) {
                int[] poll = queue.poll();
                if(poll[0] == m - 1 && poll[1] == n - 1) {
                    return count + 1;
                }
                for(int[] dir: directions) {
                    int x = dir[0] + poll[0];
                    int y = dir[1] + poll[1];
                    if(x >= 0 && x < m && y >= 0 && y < n && grid[x][y] == 0 && !visited[x][y]) {
                        queue.add(new int[]{x, y});
                        visited[x][y] = true;
                    }
                }
            }
            count++;
        }
        return -1;
    }
}
```
## 2. (279) Perfect Squares
[leetcode](https://leetcode.com/problems/perfect-squares/)
```java
class Solution {
    public int numSquares(int n) {
        //13 = 4 + 9 = 2^2 + 3^2
        /* 1 4 9 -> 2 5 10 
                 -> 5 8 13(x)
                 -> 10 13(x)
         */
        /*
        start from node 0 in the queue, then keep pushing perfect number + curr number, once we reach to n, we got the result. meanwhile we need to count
        */
        Queue<Integer> queue = new LinkedList<>();
        Set<Integer> visited = new HashSet<>();
        queue.add(0);
        visited.add(0);
        int count = 1;
        
        while(!queue.isEmpty()) {
            int size = queue.size();
            
            for(int i = 0; i< size; i++) {
                int top = queue.poll();
 
                for(int j = 1; j * j <= n; j++) {
                    int curr = top + j * j;
                    if(curr == n) {
                        return count;
                    }
                    else if(curr > n) {
                        break;
                    }
                    else if(!visited.contains(curr)) {
                        queue.add(curr);
                        visited.add(curr);
                    }
                }
            }
            count++;
        }
        return count;
    }
}

```
## 3.(127) Word Ladder
[leetcode](https://leetcode.com/problems/word-ladder/)
```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
/*
d*g=[dog], c*g=[cog], 

ho*=[hot], *og=[dog, log, cog], h*t=[hot], 
lo*=[lot, log], l*t=[lot], l*g=[log], 

do*=[dot, dog], *ot=[hot, dot, lot], d*t=[dot], 
co*=[cog]}

*/
        int L = beginWord.length();
        Map<String, List<String>> allCombo = new HashMap<>();
        //1. Transform
        for(String word: wordList) {
            for(int i = 0; i < word.length(); i++) {
                String newWord = word.substring(0, i) + "*" + word.substring(i+1);
                List<String> transformations = allCombo.getOrDefault(newWord, new ArrayList<>());
                transformations.add(word);
                allCombo.put(newWord, transformations);
            }
        }
        System.out.println(allCombo);
 
        //2. BFS
        Queue<Pair<String, Integer>> queue = new LinkedList<>();
        queue.add(new Pair(beginWord, 1));
        
        Map<String, Boolean> visited = new HashMap<>();
        visited.put(beginWord, true);
        
        while(!queue.isEmpty()) {
            Pair<String, Integer> node = queue.poll();
            String word = node.getKey();
            int level = node.getValue();
            for(int i = 0; i < L; i++) {
                String newWord = word.substring(0, i) +  "*" + word.substring(i + 1);
                for(String adj: allCombo.getOrDefault(newWord, new ArrayList<>())) {
                    if(adj.equals(endWord)) {
                        return level + 1;
                    }
                    if(!visited.containsKey(adj)) {
                        queue.add(new Pair(adj, level + 1));
                        visited.put(adj, true);
                    }
                }
            }
        }
        return 0;
    }
}
```

 
 
# DFS (Depth first search)
1. 到达一个节点，然后对这个节点进行彻底的搜索，一直到底。
2. 然后再返回到原节点，对下个邻居进行彻底搜索
3. DFS常常来求“可达性”问题。
4. 用 Stack: DFS uses a Stack to remember where it should go when it reaches a dead end.
5. Visited[] 和BFS一样。
## 1. (1239) Maximum Length of a Concatenated String with Unique Characters
![Untitled (Draft)-1](https://user-images.githubusercontent.com/19642027/93666920-0f586380-fa50-11ea-99ec-d02bae389f94.jpg)
[leetcode](https://leetcode.com/problems/maximum-length-of-a-concatenated-string-with-unique-characters/)
```java
class Solution {
    int longest = 0;
    public int maxLength(List<String> arr) {
        DFS(arr, "",0);
        return longest;
    }
    private void DFS(List<String> arr, String newStr, int index) {
        if(isUnique(newStr)){
            longest = Math.max(newStr.length(), longest);
        }
        if(index == arr.size() || !isUnique(newStr) ) {
            return;
        }
        for(int i = index; i < arr.size(); i++) {
            DFS(arr, newStr + arr.get(i), i + 1);
        }
    }
    private boolean isUnique(String s) {
        
        int[] arr = new int[26];
        for(char c: s.toCharArray()){
            arr[c - 'a']++;
        }
        for(int i: arr) {
            if(i >= 2) return false;
        }
        return true;
    }
}
```
