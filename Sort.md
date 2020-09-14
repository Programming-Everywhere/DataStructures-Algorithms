- 1 215. Kth Largest Element in an Array
- 2 347. Top K Frequent Elements

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
      return i;
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
# 2.Top K Frequent Elements
[leetcode](https://leetcode.com/problems/top-k-frequent-elements/description/)
```java
//1. PQ to add keys as the value's increasing order, then add to pq, whenever pq is more than k, then pop, rest of pq will be the result. Top K.
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> map = new HashMap<>();
        for(int i: nums) {
            map.put(i, map.getOrDefault(i, 0) + 1);
        }
        PriorityQueue<Integer> pq = new PriorityQueue<>((a, b) -> map.get(a) - map.get(b));
        for(int key: map.keySet()) {
            pq.add(key);
            if(pq.size() > k) {
                pq.poll();
            }
        }
        int[] res = new int[k];
        int j = 0;
        while(!pq.isEmpty()) {
            res[j] = pq.poll();
            j++;
        }
        return res;
    }
}

/**2. Put all same value,(frenquency) keys into the same bucket. 
Now the bucket will have the same keys with same frenquency. 
Keep in mind, the value is the index of bucket
*/
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> map = new HashMap<>();
        for(int i: nums) {
            map.put(i, map.getOrDefault(i, 0) + 1);
        }
        
        List<Integer>[] buckets = new ArrayList[nums.length + 1];
        for(int key: map.keySet()) {
            int value = map.get(key);
            if(buckets[value] == null) {
                buckets[value] = new ArrayList<>();
            }
            buckets[value].add(key);
        }
        // value is the index!
        int[] res = new int[k];
        int j = 0;
        for(int i = nums.length; i >= 0; i--) {
            if(buckets[i] == null) {
                continue;
            }
            else {
                for(int l: buckets[i]) {
                    res[j] = l;
                    j++;
                }
                if(j ==k) break;
            }
        }
        return res; 
    }
}
```
# 3. Sort Colors 荷兰国企问题 三个pointers
[leetcode](https://leetcode.com/problems/sort-colors/)
```java
class Solution {
    public void sortColors(int[] nums) {
        int zero = 0, one = 0, two = nums.length - 1;
        while(one <= two) {
            if(nums[one] == 0) {
                swap(nums,zero, one);
                zero++;
                one++;
            }
            else if(nums[one] == 2) {
                swap(nums, two, one);
                two--;
            }
            else {
                one++;
            }
        }
    }
    private void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}
/**
zero  one  two    num[one]     nums 
0     0     5       2         [0,0,2,1,1,2]
0     0     4       0         [0,0,2,1,1,2]
1     1     4       0         [0,0,2,1,1,2]
2     2     4       2         [0,0,1,1,2,2]
2     2     3       1          [0,0,1,1,2,2]
2     3     3       1          [0,0,1,1,2,2]
done
*/
```
