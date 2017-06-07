##### Kth Smallest Number In Sorted Matrix
Given a matrix of size N x M. For each row the elements are sorted in ascending order, and for each column the elements are also sorted in ascending order. Find the Kth smallest number in it.

**Assumptions**
* the matrix is not null, N > 0 and M > 0
* K > 0 and K <= N * M

**Return**
* an array with size K containing the K smallest numbers in ascending order

**Examples**
* {{1, 3,  5,  7},
   {2, 4,  8,  9},
   {3, 5, 11, 15},
   {6, 8, 13, 18}}
* the 5th smallest number is 4
* the 8th smallest number is 6

**Answers**
Analysis:
a. what kind of data structure that this algorithm uses:
    Min Heap
b. what are actions of this algorithm step by step
    a. create a min-heap
    b. insert the top left element of the matrix (matrix[0][0]) into max-heap
    c. while the count of min-heap.poll() < k
        1. expand the first priority element in min-heap (min-heap.poll())
        2. generate all adjacency elements (matrix[i + 1][j] and matrix[i][j + 1]), put them into min-heap
    d. return the kth min-heap.poll() value

```java
public class Solution {
    private class Node extends Object implements Comparable<Node> {
        public int value, index;
        Node(int value, int index) {
            this.value = value;
            this.index = index;
        }

        @Override
        public int compareTo(Node n) {
            if (value == n.value) {
                return 0;
            }

            return value > n.value ? 1 : -1;
        }

        @Override
        public boolean equals(Object o) {
            return value == ((Node) o).value;
        }

        @Override
        public int hashCode() {
            return index;
        }
    }

    public int kthSmallest(int[][] matrix, int k) {
        int count = 0;
        int height = matrix.length;
        int width = matrix[0].length;
        PriorityQueue<Node> pq = new PriorityQueue<>();
        HashSet<Node> set = new HashSet<>();
        Node curr = new Node(matrix[0][0], 0);
        pq.offer(curr);
        set.add(curr);
        count++;

        while (pq.size() > 0 && count < k) {
            curr = pq.poll();
            count++;
            int row = curr.index / width;
            int col = curr.index % width;
            if (col + 1 < width) {
                Node right = new Node(matrix[row][col + 1], curr.index + 1);
                if (set.add(right)) {
                    pq.offer(right);
                }
            }

            if (row + 1 < height) {
                Node bottom = new Node(matrix[row + 1][col], curr.index + width);
                if (set.add(bottom)) {
                    pq.offer(bottom);
                }
            }
        }

        Node result = pq.poll();

        return result.value;
    }
}
```
