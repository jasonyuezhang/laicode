##### Selection Sort
Given an array of integers, sort the elements in the array in ascending order. The selection sort algorithm should be used to solve this problem.

**Examples**

* {1} is sorted to {1}
* {1, 2, 3} is sorted to {1, 2, 3}
* {3, 2, 1} is sorted to {1, 2, 3}
* {4, 2, -3, 6, 1} is sorted to {-3, 1, 2, 4, 6}

**Corner Cases**

* What if the given array is null? In this case, we do not need to do anything.
* What if the given array is of length zero? In this case, we do not need to do anything.

**Assumptions**
* The given array is a int array contains unsorted number. Array is not null

* Analysis
* What are actions of this algorithm
*# find the smallest element in array, move it to the front
*# start from the next element in array, repeat step 1, until all elements are sorted

* Time Complexity: O(n^2)
* Space Complexity: O(1)

```java
public class Solution {
    public void swap(int[] array, int i, int j) {
        int tmp = array[i];
        array[i] = array[j];
        array[j] = tmp;
    }
    
    public int[] solve(int[] array) {
        // null check
        if (array == null || array.length == 0) {
            return array;
        }

        int len = array.length;

        for (int i = 0; i < len - 1; i++) {
            for (int j = i + 1; j < len; j++) {
                if (array[j] < array[i]) {
                    swap(array, i, j);
                }
            }
        }

        return array;
    }
}
```
