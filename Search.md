### DFS
- [1. (1239) Maximum Length of a Concatenated String with Unique Characters](https://leetcode.com/problems/maximum-length-of-a-concatenated-string-with-unique-characters/)

### BFS 
- [1.(1091) Shortest Path in Binary Matrix](https://leetcode.com/problems/shortest-path-in-binary-matrix/)

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
 
 ```

 
 
 
# DFS (Depth first search)
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
