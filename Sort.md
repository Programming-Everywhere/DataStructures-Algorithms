# 1. Kth Element
[leetcode](https://leetcode.com/problems/kth-largest-element-in-an-array/description/)
```java
// quick sort
/** [3,2,1,5,6,4] 
1. find 4 as pivot 
2. comparing each element with pivot 4, smaller ones will be on the left, bigger ones will be on the right of pivot. 
2.5 indicator i = -1, and traverse j = 0
3. arr[j] < pivot: i++, swap (arr[i], arr[j]) -> swap(3,3), j++
4. arr[j] < pivot; i++, swap(arr[i], arr[j]) -> swap(2, 2), j++
5. arr[j] < pivot; i++, swap(arr[i], arr[j]) -> swap(1,1),  j++
6. arr[j] > pivot; j++
7. arr[j] > pivot; j++
8. swap(arr[i+1], pivot)
9, [3,2,1,4,6,5]
10. this will return i+1 the index being swap with pivot 
11. then use recursive to do left of i+1, and right of i+1
*/
class Solution {

  public int findKthLargest(int[] arr, int k) {
    k = arr.length - k;
    int low = 0, high = arr.length - 1;
    while(low < high) {
       int j = partition(arr, low, high);
       if(j == k) {
         break;
       }
       else if(j < k) {
         low = j + 1;
       }
       else {
         high = j - 1;
       }
    }
    return arr[k];
  }
  public int partition(int[] arr, int low, int high) {
      int i = low;
      int pivot = arr[high];
      for(int j = low; j < high; j++) {
         if(arr[j] < pivot) {
           swap(arr, i, j);
           i++;
         }
      }
      swap(arr, i, high);
      return i+1;
  }
  /** sort 再用
  public void sort(int[] arr, int low, int high) {
      if(low < high) {
       int index = partition(arr, low, high);
       sort(arr, low, index - 1);
       sort(arr, index + 1, high);
     }
  }
  */
  public void swap(int[] arr,int i, int j) {
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
  }
  

}

```
