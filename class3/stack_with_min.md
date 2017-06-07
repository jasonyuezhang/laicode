##### Stack With min()
Enhance the stack implementation to support min() operation. min() should return the current minimum value in the stack. If the stack is empty, min() should return -1.

* pop() - remove and return the top element, if the stack is empty, return -1
* push(int element) - push the element to top
* top() - return the top element without remove it, if the stack is empty, return -1
* min() - return the current min value in the stack.

```java
public class Solution {
    Stack<Integer> stack;
    List<Integer[]> globalMin;
    int size;

    public Solution() {
        stack = new Stack<Integer>();
        globalMin = new ArrayList<Integer[]>();
        size = 0;
    }

    public int pop() {
        if (this.size == 0) {
            return -1;
        }

        int top = stack.pop();
        if (top == min() && (globalMin.get(globalMin.size() - 1)[1]) == size - 1) {
            globalMin.remove(size - 1);
        }

        size--;
        return top;
    }

    public void push(int element) {
        if (min() == -1 || element < min()) {
            globalMin.add(new Integer[] {element, size});
        }

        stack.push(element);
        size++;
    }

    public int top() {
        if (this.size == 0) {
            return -1;
        }

        return stack.peek();
    }

    public int min() {
        if (this.size == 0) {
            return -1;
        }

        return globalMin.get(globalMin.size() - 1)[0];
    }
}
```