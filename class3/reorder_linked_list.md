##### Re-order Linked List
Reorder the given singly-linked list N1 -> N2 -> N3 -> N4 -> … -> Nn -> null to be N1- > Nn -> N2 -> Nn-1 -> N3 -> Nn-2 -> … -> null

**Examples**
* L = null, is reordered to null
* L = 1 -> null, is reordered to 1 -> null
* L = 1 -> 2 -> 3 -> 4 -> null, is reordered to 1 -> 4 -> 2 -> 3 -> null
* L = 1 -> 2 -> 3 -> null, is reordred to 1 -> 3 -> 2 -> null

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
    public ListNode findMiddle(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }

        ListNode slow = head;
        ListNode fast = head;

        while (fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        return slow;
    }

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

    public ListNode merge(ListNode a, ListNode b) {
        if (a == null && b == null) {
            return null;
        }

        ListNode head = new ListNode(0);
        ListNode curr = head;

        while (a != null && b != null) {
            curr.next = a;
            a = a.next;
            curr.next.next = b;
            b = b.next;
            curr = curr.next.next;
        }

        if (a != null) {
            curr.next = a;
        } else {
            curr.next = b;
        }

        curr = head;
        head = head.next;
        curr = null;

        return head;
    }

    public ListNode reorder(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }

        ListNode middle = findMiddle(head);
        ListNode secondHead = middle.next;
        middle.next = null;

        secondHead = reverse(secondHead);

        head = merge(head, secondHead);

        return head;
    }
}
```