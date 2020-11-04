<!-- GFM-TOC -->
* [1. IntersectionofTwoLinkedLists](#1-IntersectionofTwoLinkedLists)
* [2. ReverseLinkedList](#2-ReverseLinkedList)
* [3. MergeTwoSortedLists](#3-MergeTwoSortedLists)
<!-- GFM-TOC -->

## 1. IntersectionofTwoLinkedLists
[leetcode](https://leetcode.com/problems/intersection-of-two-linked-lists/description/)
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        /*
        a1 -> a2 
                 ↘
                  c1 -> c2 -> null
                 ↗ 
  b1 -> b2 -> b3
  1. when A is at the end, and still not intersected, then A(head) will point to headB
  2. B(head) will point to headA
  3. A!=B while loop
        */
        if(headA == null || headB == null) return null;
        ListNode A = headA, B = headB;
        while(A != B) {
            if(A == null) {
                A = headB;
            }
            else{
                A = A.next;
            }
            if(B == null) {
                B = headA;
            }
            else {
                B = B.next;
            }
        }
        return A; 
    }
}
```

## 2. ReverseLinkedList
[leetcode](https://leetcode.com/problems/reverse-linked-list/)
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        /* 1. null   1 -> 2 ->3->4->5->NULL
               *     %    $
           (res)null<-1 
           --------------------------------
           2. null  1 ->  2 ->  3->4->5->NULL
                 *     %    $
            (res)null<-1<-2 
            --------------------------------
           3. null  1 ->  2 ->  3->  4-> 5->NULL
                        *     %    $  
            (res)null<-1<-2<-3
            --------------------------------
            ....
            (res) 5->4->3->2->1->NULL
 Explanation:
        3 pointers:
        preHead, Curr, nextHead
        2. eveytime loop, just let curr.next = preHead 
        3. then move ALL 3 pointers 
        */
        ListNode preHead = null;
        ListNode curr = head;
        while(curr != null) {
            ListNode nextHead = curr.next;
            curr.next = preHead; // point to preHead
            
            //2. move 3 ptrs 
            preHead = curr;
            curr = nextHead;
        }
        return preHead;
    }
}
```
## 3. MergeTwoSortedLists
[leetcode](https://leetcode.com/problems/merge-two-sorted-lists/)
```java

```
