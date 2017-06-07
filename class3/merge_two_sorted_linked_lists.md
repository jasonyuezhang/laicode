##### Merge Two Sorted Linked Lists

Merge two sorted lists into one large sorted list.

**Examples**
* L1 = 1 -> 4 -> 6 -> null, L2 = 2 -> 5 -> null, merge L1 and L2 to 1 -> 2 -> 4 -> 5 -> 6 -> null
* L1 = null, L2 = 1 -> 2 -> null, merge L1 and L2 to 1 -> 2 -> null
* L1 = null, L2 = null, merge L1 and L2 to null

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
    public ListNode merge(ListNode one, ListNode two) {
        if (one == null && two == null) {
            return null;
        }

        ListNode head = new ListNode(0);
        ListNode curr = head;

        while (one != null && two != null) {
            if (one.value <= two.value) {
                curr.next = one;
                one = one.next;
            } else {
                curr.next = two;
                two = two.next;
            }
            curr = curr.next;
        }

        if (one != null) {
            curr.next = one;
        } else if (two != null) {
            curr.next = two;
        }

        curr = head;
        head = head.next;
        curr.next = null;

        return head;
    }
}
```
