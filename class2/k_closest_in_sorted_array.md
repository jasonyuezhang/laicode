##### K Closest In Sorted Array
Given a target integer T, a non-negative integer K and an integer array A sorted in ascending order, find the K closest numbers to T in A.

**Assumptions**
* A is not null
* K is guranteed to be >= 0 and K is guranteed to be <= A.length

**Return**
* A size K integer array containing the K closest numbers(not indices) in A, sorted in ascending order by the difference between the number and T. 

**Examples**
* A = {1, 2, 3}, T = 2, K = 3, return {2, 1, 3} or {2, 3, 1}
* A = {1, 4, 6, 8}, T = 3, K = 3, return {4, 1, 6}

```java
public class Solution {
    public int[] kClosest(int[] array, int target, int k) {
        // null and empty array check
        if (array == null || array.length == 0) {
            return array;
        }

        if (k == 0) {
            return new int[0];
        }

        int start = 0;
        int end = array.length - 1;
        int mid = (start + end) / 2;
        int closest = -1;

        // find the range contains closest element
        while (start < end - 1) {
            if (target == array[mid]) {
                closest = mid;
                break;
            } else if (target < array[mid]) {
                end = mid;
            } else {
                start = mid;
            }
            mid = (start + end) / 2;
        }

        // decide the closest element
        if (target - array[start] > array[end] - target) {
            closest = end;
        } else {
            closest = start;
        }

        int[] result = new int[k];
        result[0] = array[closest];
        int i = closest - 1;
        int j = closest + 1;

        for (int count = 1; count < k && (i >= 0 || j < array.length); count++) {
            if (i < 0) {
                result[count] = array[j++];
            } else if (j >= array.length) {
                result[count] = array[i--];
            } else if (target - array[i] > array[j] - target) {
                result[count] = array[j++];
            } else {
                result[count] = array[i--];
            }
        }

        return result;
    }
}
```
