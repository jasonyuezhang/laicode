##### Last Occurence
Given a target integer T and an integer array A sorted in ascending order, find the index of the last occurrence of T in A or return -1 if there is no such index.

**Assumptions**
* There can be duplicate elements in the array.

**Examples**
* A = {1, 2, 3}, T = 2, return 1
* A = {1, 2, 3}, T = 4, return -1
* A = {1, 2, 2, 2, 3}, T = 2, return 3

**Corner Cases**
* What if A is null or A is array of zero length? We should return -1 in this case.

```java
public class Solution {
    public int lastOccur(int[] array, int target) {
        // null parameter or empty array check
        if (array == null || array.length == 0) {
            return -1;
        }

        // initial local variables
        int start = 0;
        int end = array.length - 1;
        int mid = (start + end) / 2;

        // shirnk boundary
        while (start < end - 1) {
            mid = (start + end) / 2;
            if (target == array[mid]) {
                start = mid;
            } else if (target < array[mid]) {
                end = mid - 1;
            } else {
                start = mid + 1;
            }
        }

        // post-process
        if (end > 0 && array[end] == target) {
            return end;
        } else if (start < array.length && array[start] == target) {
            return start;
        }

        return -1;
    }
}
```
