##### Merge Sort

Given an array of integers, sort the elements in the array in ascending order. The merge sort algorithm should be used to solve this problem.

**Examples**

* {1} is sorted to {1}
* {1, 2, 3} is sorted to {1, 2, 3}
* {3, 2, 1} is sorted to {1, 2, 3}
* {4, 2, -3, 6, 1} is sorted to {-3, 1, 2, 4, 6}

**Corner Cases**

* What if the given array is null? In this case, we do not need to do anything.
* What if the given array is of length zero? In this case, we do not need to do anything.

**Assumptions**
The given array is a not null unsorted int array.

**Analysis
* if it is only one element in the array, it's already sorted, return.
* divide the array recursively into two halves until it can no more be divided.
* merge the smaller array into new array in sorted order

**Complexity**
* Time: O(nlogn)
* Space: O(n)

```java
public class Solution {
    public int[] mergeSort(int[] array) {
        int[] helper = new int[array.length];
        mergeSort(array, helper, 0, array.length - 1);
        return array;
    }

    public void mergeSort(int[] array, int[] helper, int left, int right) {
        if (left >= right) {
            return;
        }
        int mid = left + (right - left) / 2;
        mergeSort(array, helper, left, mid);
        mergeSort(array, helper, mid + 1, right);
        combine(array, helper, left, mid, right);
    }

    public void combine(int[] array, int[] helper, int left, int mid, int right) {
        // if right array has element unsorted, they are at the right position already
        // copy target section into helper array
        for (int i = left; i <= right; i++) {
            helper[i] = array[i];
        }

        int leftIndex = left;
        int rightIndex = mid + 1;

        while(leftIndex <= mid && rightIndex <= right) {
            if (helper[leftIndex] < helper[rightIndex]) {
                array[left++] = helper[leftIndex++];
            } else {
                array[left++] = helper[rightIndex++];
            }
        }

        // if left array has element unsorted
        while (leftIndex <= mid && left <= right) {
            array[left++] = helper[leftIndex++];
        }
    }
}
```
