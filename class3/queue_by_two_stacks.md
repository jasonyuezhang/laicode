##### Queue by Two Stacks
Java: Implement a queue by using two stacks. The queue should provide size(), isEmpty(), offer(), poll() and peek() operations. When the queue is empty, poll() and peek() should return null.

C++: Implement a queue by using two stacks. The queue should provide size(), isEmpty(), push(), front() and pop() operations. When the queue is empty, front() should return -1.

**Assumptions**
* The elements in the queue are all Integers.
size() should return the number of elements buffered in the queue.
isEmpty() should return true if there is no element buffered in the queue, false otherwise.

```java
public class Solution {
    private Stack<Integer> stack1, stack2
    private int size;

    public Solution() {
        stack1 = new Stack<Integer>();
        stack2 = new Stack<Integer>();
        size = 0;
    }

    private void reload() {
        if (this.size == 0) {
            return;
        }

        // if stack2 is empty, reload stack2 with all elements in stack1
        if (stack2.empty()) {
            while (!stack1.empty()) {
                // move all elements in stack 1 to stack 2
                stack2.push(stack1.pop());
            }
        }
    }


    public Integer poll() {
        if (isEmpty()) {
            return null;
        }

        reload();
        this.size--;
        return stack2.pop();
    }

    public void offer(int element) {
        stack1.push(element);
        this.size++;
    }

    public Integer peek() {
        if (isEmpty()) {
            return null;
        }

        reload();
        return stack2.peek();
    }

    public int size() {
        return this.size;
    }

    public boolean isEmpty() {
        return this.size == 0;
    }
}
```