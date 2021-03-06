### BFS 
- [1.(1091) Shortest Path in Binary Matrix](https://leetcode.com/problems/shortest-path-in-binary-matrix/)
- [2.(279) Perfect Squares](https://leetcode.com/problems/perfect-squares/)
- [3.(127) Word Ladder](https://leetcode.com/problems/word-ladder/)

### DFS
- [1.(1239) Maximum Length of a Concatenated String with Unique Characters](https://leetcode.com/problems/maximum-length-of-a-concatenated-string-with-unique-characters/)
- [2.(695) Max Area of Island](https://leetcode.com/problems/max-area-of-island/description/)
- [3.(200) Number of Islands](https://leetcode.com/problems/number-of-islands/)
- [4.(547) Friend Circles](https://leetcode.com/problems/friend-circles/)
- [5.(130) Surrounded Regions](https://leetcode.com/problems/surrounded-regions/description/)
- [6.(417) Pacific Atlantic Water Flow](https://leetcode.com/problems/pacific-atlantic-water-flow/description/)

### Backtracking
- [1.(17) Letter Combinations of a Phone Number (Medium)](https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/)
- [[WIP]2.(93) Restore IP Addresses](https://leetcode.com/problems/restore-ip-addresses/description/)
- [3.(79) Word Search ](https://leetcode.com/problems/word-search/)
- [4.(257) Binary Tree Paths](https://leetcode.com/problems/binary-tree-paths/description/)
- [5.(46) Permutations](https://leetcode.com/problems/permutations/)

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
## 2.(695) Max Area of Island
[leetcode](https://leetcode.com/problems/max-area-of-island/description/)
```java
//BFS
class Solution {
    int[][] directions = {{1,0},{-1,0},{0,1},{0,-1}};
    public int maxAreaOfIsland(int[][] grid) {
        if(grid.length == 0 || grid == null) return 0;
        int m = grid.length;
        int n = grid[0].length;
        int count = 0, res = 0;
        boolean[][]visited = new boolean[m][n];
        for(int i = 0; i < m; i++) {
            for(int j = 0; j < n; j++) {
                if(grid[i][j] == 1 && !visited[i][j]) {
                    count = BFS(grid, i, j, visited);
                    res = Math.max(res, count);
                }
            }
        }
        return res;
    }
    private int BFS(int[][] grid, int row, int col, boolean[][] visited) {
        Queue<int[]> queue = new LinkedList<>();
        queue.add(new int[]{row, col});
        visited[row][col] = true;
        int res = 0;
        while(!queue.isEmpty()) {
            int[] curr = queue.poll();
            res++;
            for(int[] dir: directions) {
                int x = dir[0] + curr[0];
                int y = dir[1] + curr[1];
                if(x < grid.length && x >= 0 && y < grid[0].length && y >= 0 &&
                  !visited[x][y] && grid[x][y] == 1) {
                    queue.add(new int[]{x, y});
                    visited[x][y] = true;
                }
            }
        }
        return res;
    }
}

//DFS
class Solution {
    int count = 0;
    int res = 0;
    public int maxAreaOfIsland(int[][] grid) {
        boolean[][] visited = new boolean[grid.length][grid[0].length];
        for(int i = 0; i < grid.length; i++) {
            for(int j = 0; j < grid[0].length; j++) {
                if(grid[i][j] == 1) {
                    count = 0;
                    DFS(grid, i, j, visited);
                    visited[i][j] = true;
                }
            }
        }
        return res;
    }
    private void DFS(int[][] grid, int row, int col, boolean[][] visited) {
        if(row < 0 || row >= grid.length || col < 0 || col >= grid[0].length || grid[row][col] != 1 || visited[row][col]) {
            return;
        }
        //1. modified the original input: grid[row][col] = -1;
        visited[row][col] = true;
        count++;
        DFS(grid, row+1, col,visited );
        DFS(grid, row-1, col,visited);
        DFS(grid, row, col+1,visited);
        DFS(grid, row, col-1,visited);
        
        res = Math.max(res, count);
    }
}
```

## 3.(200) Number of Islands
[leetcode](https://leetcode.com/problems/number-of-islands/)
```java
//DFS
class Solution {
    public int numIslands(char[][] grid) {
        if( grid.length == 0 || grid == null) return 0;
        int m = grid.length;
        int n = grid[0].length;
        int count = 0;
        boolean[][] visited = new boolean[m][n];
        for(int i = 0; i < m; i++) {
            for(int j = 0; j < n; j++) {
                if(grid[i][j] == '1' && !visited[i][j]) {
                    DFS(grid, i, j, visited);
                    count++;
                }
            }
        }
        return count;
    }
    private void DFS(char[][] grid, int row, int col, boolean[][] visited) {
        if(row < 0 || row >= grid.length || col < 0 || col >= grid[0].length || grid[row][col] != '1' || visited[row][col] ) {
            return;
        }
        visited[row][col] = true;
        DFS(grid,row+1, col,visited);
        DFS(grid,row-1, col,visited);
        DFS(grid,row, col+1,visited);
        DFS(grid,row, col-1,visited);
    }
}
//BFS
class Solution {
    int[][] directions = {{-1,0},{1,0},{0,-1},{0,1}};
    public int numIslands(char[][] grid) {
        if(grid.length == 0 || grid == null) return 0;
        
        boolean[][] visited = new boolean[grid.length][grid[0].length];
        int count = 0;
        for(int i = 0; i < grid.length; i++) {
            for(int j = 0; j < grid[0].length; j++) {
                if(!visited[i][j] && grid[i][j] == '1') {
                    BFS(grid, i, j, visited);
                    count++;
                }
            }
        }
        return count;
    }
    
    private void BFS(char[][] grid, int i, int j, boolean[][] visited) {
        
        Queue<int[]> queue = new LinkedList<>();
        queue.add(new int[]{i,j});
        visited[i][j] = true;
        
        while(!queue.isEmpty()) {
            int[] poll = queue.poll();
            for(int[] dir: directions) {
                int x = dir[0] + poll[0];
                int y = dir[1] + poll[1];
                if(x >= 0 && x < grid.length && y >= 0 && y < grid[0].length && grid[x][y] == '1' && !visited[x][y]) {
                    queue.add(new int[]{x, y});
                    visited[x][y] = true;
                }
            }
        }
    }
}
```
## 4. (547) Friend Circles
[leetcode](https://leetcode.com/problems/friend-circles/)
```java
//DFS
class Solution {
    public int findCircleNum(int[][] M) {
       /*
         [1,1,0], ->row = 0, M[0][0] = 1, M[0][1]=1, 0->(0,1)
         [1,1,1], ->row = 1, M[1][0] = 1, M[1][1]=1,M[1][2]=1 1->(0,1,2)
         [0,1,1]  ->row = 2, M[2][1] = 1, M[2][2]=1, 2->(1,2)
         
          0->(1) 
          1->(0,2)
          2->(1)
       */
        boolean[] visited = new boolean[M.length];
        int count = 0;
        for(int row = 0; row < M.length; row++) {
            if(!visited[row]) {
                DFS(M, row, visited);
                count++;
            }
        }
        return count;
    }
    private void DFS(int[][] M, int row, boolean[] visited) {
        for(int col = 0; col < M[0].length; col++) {
            if(M[row][col] == 0) continue;
            else if(M[row][col] == 1 && !visited[col]) {
                visited[col] = true;
                DFS(M, col, visited);
                
            }
        }
    }
}
//BFS
class Solution {
    public int findCircleNum(int[][] M) {

        boolean[] visited = new boolean[M.length];
        Queue<Integer> queue = new LinkedList<>();
        int count = 0;
        
        for(int row = 0; row < M.length; row++) {
            if(!visited[row]) {
                queue.add(row);
                
                while(!queue.isEmpty()) {
                    int poll = queue.poll();
                    visited[poll] = true;
                    
                    for(int col = 0; col < M[0].length; col++) {
                        if(M[poll][col] == 1 && !visited[col]) {
                            queue.add(col);
                        }
                    }
                }
                count++;
            }
        }
        return count;
    }
}
```
## 5. (130) Surrounded Regions
[leetcode](https://leetcode.com/problems/surrounded-regions/description/)
```java
//DFS
class Solution {
    public void solve(char[][] board) {
        if(board.length == 0 || board[0].length == 0 || board.length < 3 || board[0].length < 3 ){
            return;
        }
        int m = board.length;
        int n = board[0].length;
        // scan the first last col
        for(int i = 0; i < m; i++) {
            if(board[i][0] == 'O') {
                DFS(board, i, 0);
            }
            if(board[i][n - 1] == 'O') {
                DFS(board, i, n - 1);
            }
        }
        //scan the first and last row
         for(int i = 0; i < n; i++) {
             if(board[0][i] == 'O') {
                 DFS(board, 0, i);
             }
              if(board[m-1][i] == 'O') {
                 DFS(board, m - 1, i);
             }
         }
        for(int i = 0; i < m; i++) {
            for(int j = 0; j < n; j++) {
                if(board[i][j] == 'O') {
                    board[i][j] = 'X';
                }
                if(board[i][j] == '*') {
                    board[i][j] = 'O';
                }
            }
        }
    }
    private void DFS(char[][] board, int row, int col) {
        if(row < 0 || row >= board.length || col < 0 || col >= board[0].length ||
          board[row][col] != 'O') {
            return;
        }
        board[row][col] = '*';
        DFS(board, row+1, col);
        DFS(board, row-1, col);
        DFS(board, row, col+1);
        DFS(board, row, col-1);
    }
}
```
## 6.(417) Pacific Atlantic Water Flow
[leetcode](https://leetcode.com/problems/pacific-atlantic-water-flow/description/)
```java
class Solution {
    int[][] dir = {{1,0},{-1,0},{0,1},{0,-1}};
    public List<List<Integer>> pacificAtlantic(int[][] matrix) {
        List<List<Integer>> res = new ArrayList();
        if(matrix.length == 0 || matrix == null) return res;
        
        Queue<int[]> pBoarder = new LinkedList<>();
        Queue<int[]> aBoarder = new LinkedList<>();
        boolean[][] pVisited = new boolean[matrix.length][matrix[0].length];
        boolean[][] aVisited = new boolean[matrix.length][matrix[0].length];
        int row = matrix.length, col = matrix[0].length;
        //fill vertical 
        for(int i = 0; i < row; i++) {
            pBoarder.add(new int[] {i, 0});
            aBoarder.add(new int[] {i, col - 1});
            pVisited[i][0] = true;
            aVisited[i][col - 1] = true;
        }
        //fill horizontal
        for(int i = 0; i < col; i++) {
            pBoarder.add(new int[] {0, i});
            aBoarder.add(new int[] {row - 1, i});
            pVisited[0][i] = true;
            aVisited[row-1][0] = true;
        }
        BFS(matrix, pBoarder, pVisited);
        BFS(matrix, aBoarder, aVisited);
        for(int i = 0; i < row; i++) {
            for(int j = 0; j < col; j++) {
                if(pVisited[i][j] && aVisited[i][j]) {
                    List<Integer> cur = new ArrayList<>();
                    cur.add(i);
                    cur.add(j);
                    res.add(cur);
                }
            }
        }
        return res;
    }
    private void BFS(int[][] matrix, Queue<int[]> queue, boolean[][] visited ) {
        while(!queue.isEmpty()) {
            int[] poll = queue.poll();
            for(int[] d: dir) {
                int x = poll[0] + d[0];
                int y = poll[1] + d[1];
                if(x >= 0 && x < matrix.length && y >= 0 && y < matrix[0].length && matrix[x][y] >= matrix[poll[0]][poll[1]] && !visited[x][y]) {
                    visited[x][y] = true;
                    queue.add(new int[]{x, y});
                }
            }
        }
    }
}
```
# Backtracking
- DFS is for a questions are 'Reachable', bakctracking is for 'get some point then return' 
- backtracking mainly is for 'Permutations'. ie: {'a', 'b', 'c'} -> every permutation of this.
- need Visited[] to make sure no re-visited
- but when in recursive, it should mark it as non-visited.
## 1.(17) Letter Combinations of a Phone Number (Medium)
[leetcode](https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/)
```java
class Solution {
    Map<String, String> map = new HashMap<>(){{
         put("2",  "abc");
         put("3",  "def");
         put("4",  "ghi");
         put("5",  "jkl");
         put("6",  "mno");
         put("7",  "pqrs");
         put("8",  "tuv");
         put("9",  "wxyz");
    }};
    public List<String> letterCombinations(String digits) {
        List<String> res = new ArrayList<>();
        if(digits.length() == 0) return res;
        Backtrack(res, "", digits);
        return res;
    }
    private void Backtrack(List<String> res, String curr, String digits) {
        if(digits.length() == 0) {
            res.add(curr);
        }
        else {
            String nextDigit = digits.substring(0, 1); // 2 
            String letters = map.get(nextDigit); // abc 
            for(int i = 0; i < letters.length(); i++) {
                Backtrack(res, curr + letters.substring(i, i + 1), digits.substring(1));
            }
        }
    }
}
```
## 2.(93) Restore IP Addresses
[leetcode](https://leetcode.com/problems/restore-ip-addresses/description/)
```java
```

## 3.(79) Word Search 
[leetcode](https://leetcode.com/problems/word-search/)
```java
class Solution {
    public boolean exist(char[][] board, String word) {
        if(board == null || board[0].length == 0) return false;
        int m = board.length;
        int n = board[0].length;
        boolean[][] visited = new boolean[m][n];
        
        for(int i = 0; i < m; i++) {
            for(int j = 0; j < n; j++) {
                if(DFS(board, visited, i, j, 0, word)) {
                    return true;
                }
            }
        }
        return false;
    }
    private boolean DFS(char[][] board,boolean[][] visited, int x, int y, int index,String word) {
        if(index == word.length()) return true;
        
        if(x < 0 || x >= board.length || y < 0 || y >= board[0].length ||
          board[x][y] != word.charAt(index) || visited[x][y]) {
            return false;
        }
        visited[x][y] = true;
        if(DFS(board, visited, x + 1, y, index + 1, word) ||
          DFS(board, visited, x - 1, y, index + 1, word) ||
          DFS(board, visited, x, y + 1, index + 1, word) ||
          DFS(board, visited, x, y - 1, index + 1, word)) {
            return true;
        }
        visited[x][y] = false;
        return false;
    }
}
```
## 4.(257) Binary Tree Paths
[leetcode](https://leetcode.com/problems/binary-tree-paths/description/)
```java
class Solution {
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> res = new ArrayList<>();
        if(root == null) return res;
        StringBuilder sb = new StringBuilder();
        helper(res, root, sb);
        return res;
    }
    private void helper(List<String> res, TreeNode root, StringBuilder sb) {
        if(root == null) {
            return;
        }
        int len = sb.length();
        sb.append(root.val);
        if(root.left == null && root.right == null) {
            res.add(sb.toString());
        }
        else {
            sb.append("->");
            helper(res, root.left, sb);
            helper(res, root.right, sb);
        }
        sb.setLength(len);
    }
}
```
## 5.(46) Permutations
[leetcode](https://leetcode.com/problems/permutations/)
```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> current = new ArrayList<>();
        for(int n: nums) {
            current.add(n);
        }
        backtrack(nums.length, res, current, 0);
        return res;
    }
    private void backtrack(int n, List<List<Integer>> res, List<Integer> current, int first) {
        if(first == n) {
            res.add(new ArrayList<>(current));
        }
        else {
            for(int i = first; i < n; i++) {
                Collections.swap(current, first, i);
                backtrack(n, res, current, first + 1);
                Collections.swap(current, first, i);
            }
        }
    }
}
```



