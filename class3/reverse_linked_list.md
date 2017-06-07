##### Reverse Linked List
Reverse a singly-linked list.

**Examples**
* L = null, return null
* L = 1 -> null, return 1 -> null
* L = 1 -> 2 -> 3 -> null, return 3 -> 2 -> 1 -> null

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
    public ListNode reverse(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }

        ListNode revHead = null;
        ListNode curr = null;

        while (head != null) {
            curr = head;
            head = head.next;
            curr.next = revHead;
            revHead = curr;
        }

        return revHead;
    }
}
```
