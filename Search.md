# DFS
- [1. (1239) Maximum Length of a Concatenated String with Unique Characters](https://leetcode.com/problems/maximum-length-of-a-concatenated-string-with-unique-characters/)

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
