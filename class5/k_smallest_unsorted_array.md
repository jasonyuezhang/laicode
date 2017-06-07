##### K Smallest In Unsorted Array
Find the K smallest numbers in an unsorted integer array A. The returned numbers should be in ascending order.

**Assumptions**
* A is not null
* K is >= 0 and smaller than or equal to size of A

**Return**
* an array with size K containing the K smallest numbers in ascending order

**Examples**
* A = {3, 4, 1, 2, 5}, K = 3, the 3 smallest numbers are {1, 2, 3}

**Answers**
Analysis:
a. what kind of data structure that this algorithm uses:
    Max Heap
b. what are actions of this algorithm step by step
    a. create a max-heap
    b. insert first k elements of array into heap
    c. iterate the rest of n-k elements
        1. insert the element into max-heap
        2. pop the max element in max-heap
    d. return the max-heap as array

```java
public class Solution {
    public int[] kSmallest(int[] array, int k) {
        if (array == null || array.length == 0) {
            return array;
        }

        if (k == 0) {
            return new int[0];
        }

        int[] result = new int[k];

        PriorityQueue<Integer> pq = new PriorityQueue<>(k + 1, Collections.reverseOrder());

        for (int n : array) {
            pq.offer(n);
            if (pq.size() > k) {
                pq.poll();
            }
        }

        for (int i = k - 1; i >= 0; i--) {
            result[i] = pq.poll();
        }

        return result;
    }
}
```

```java
public class Solution {
    public int[] kSmallest(int[] array, int k) {
        if (array == null || array.length == 0) {
            return array;
        }

        if (k == 0) {
            return new int[0];
        }

        int[] result = new int[k];

        PriorityQueue<Integer> pq = new PriorityQueue<>(k + 1, new Comparator<Integer>() {
            @Override
            public int compare(Integer x, Integer y) {
              if (x == y) {
                return 0;
              }
              return x > y ? -1 : 1;
            }
        });

        for (int n : array) {
            pq.offer(n);
            if (pq.size() > k) {
                pq.poll();
            }
        }

        for (int i = k - 1; i >= 0; i--) {
            result[i] = pq.poll();
        }

        return result;
    }
}
```
