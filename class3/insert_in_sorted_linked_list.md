##### Insert In Sorted Linked List
Insert a value in a sorted linked list.

**Examples**
* L = null, insert 1, return 1 -> null
* L = 1 -> 3 -> 5 -> null, insert 2, return 1 -> 2 -> 3 -> 5 -> null
* L = 1 -> 3 -> 5 -> null, insert 3, return 1 -> 3 -> 3 -> 5 -> null
* L = 2 -> 3 -> null, insert 1, return 1 -> 2 -> 3 -> null

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
    public ListNode insert(ListNode head, int value) {
        ListNode newNode = new ListNode(value);

        if (head == null) {
            return newNode;
        }

        if (value < head.value) {
            newNode.next = head;
            head = newNode;
            return head;
        }

        ListNode curr = head;

        while (curr.next != null) {
            if (curr.value <= value && curr.next.value >= value) {
                newNode.next = curr.next;
                curr.next = newNode;
                return head;
            }
            curr = curr.next;
        }

        curr.next = newNode;
        return head;
    }
}
```
