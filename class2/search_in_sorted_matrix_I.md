##### Search In Sorted Matrix I
Given a 2D matrix that contains integers only, which each row is sorted in an ascending order. The first element of next row is larger than (or equal to) the last element of previous row.

Given a target number, returning the position that the target locates within the matrix. If the target number does not exist in the matrix, return {-1, -1}.

**Assumptions:**
* The given matrix is not null, and has size of N * M, where N >= 0 and M >= 0.

**Examples:**
* matrix = { {1, 2, 3}, {4, 5, 7}, {8, 9, 10} }
* target = 7, return {1, 2}
* target = 6, return {-1, -1} to represent the target number does not exist in the matrix.

```java
public class Solution {
    public int[] search(int[][] matrix, int target) {
        int height = matrix.length;
        int[] notFound = new int[] {-1, -1};

        if (height == 0) {
            return notFound;
        }

        int width = matrix[0].length;

        if (width == 0) {
            return notFound;
        }

        int start = 0;
        int end = height * width - 1;
        int mid, row, col;

        while (start <= end) {
            mid = (start + end) / 2;
            row = mid / width;
            col = mid % width;

            if (target == matrix[row][col]) {
                return new int[] {row, col};
            } else if (target < matrix[row][col]) {
                end = mid - 1;
            } else {
                start = mid + 1;
            }
        }

        return notFound;
    }
}
```