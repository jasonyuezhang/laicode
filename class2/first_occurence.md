##### First Occurence
Given a target integer T and an integer array A sorted in ascending order, find the index of the first occurrence of T in A or return -1 if there is no such index.

**Assumptions**
* here can be duplicate elements in the array.

**Examples**
* A = {1, 2, 3}, T = 2, return 1
* A = {1, 2, 3}, T = 4, return -1
* A = {1, 2, 2, 2, 3}, T = 2, return 1

**Corner Cases**
* What if A is null or A of zero length? We should return -1 in this case.

```java
public class Solution {
    public int firstOccur(int[] array, int target) {
        // null parameter and empty array check
        if (array == null || array.length == 0) {
            return -1;
        }

        int start = 0;
        int end = array.length - 1;
        int mid = (start + end) / 2;

        while (start < end - 1) {
            mid = (start + end) / 2;

            if (array[mid] == target) {
                end = mid;
            } else if (target < array[mid]) {
                end = mid - 1;
            } else {
                start = mid + 1;
            }
        }

        // post-process
        if (start < array.length && array[start] == target) {
            return start;
        } else if (end > 0 && array[end] == target) {
            return end;
        }
        return -1;
    }
}
```
