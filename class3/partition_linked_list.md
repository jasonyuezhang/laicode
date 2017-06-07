##### Partition Linked List
Given a linked list and a target value T, partition it such that all nodes less than T are listed before the nodes larger than or equal to target value T. The original relative order of the nodes in each of the two partitions should be preserved.

**Examples**
* L = 2 -> 4 -> 3 -> 5 -> 1 -> null, T = 3, is partitioned to 2 -> 1 -> 4 -> 3 -> 5 -> null

```java
/**
 * class ListNode {
 *   public int value;
 *   public ListNode next;
 *   public ListNode(int value) {
 *     this.value = value;
 *     next = null;
 *   }
 * }
 */
public class Solution {
    public ListNode partition(ListNode head, int target) {
        if (head == null || head.next == null) {
            return head;
        }

        ListNode headLess = new ListNode(0);
        ListNode currLess = headLess;
        ListNode headGreater = new ListNode(0);
        ListNode currGreater = headGreater;
        ListNode curr = head;
        ListNode prev = null;

        while (curr != null) {
            if (curr.value < target) {
                currLess.next = curr;
                currLess = currLess.next;
            } else {
                currGreater.next = curr;
                currGreater = currGreater.next;
            }
            prev = curr;
            curr = curr.next;
            prev.next = null;
        }

        currLess.next = headGreater.next;
        currLess = headLess.next;

        // detach dummy node
        headLess.next = null;
        headGreater.next = null;

        return currLess;
    }
}
```
