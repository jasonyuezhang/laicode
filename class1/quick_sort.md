#### Quick Sort
```java
public class Solution {
    // swap two array elements
    private void swap (int[] array, int i, int j) {
        int tmp = array[i];
        array[i] = array[j];
        array[j] = tmp;
    }

    // end is exclusive
    public void quickSort(int[] array, int start, int end) {
        // base case
        if (start >= end - 1) {
            return;
        }
        
        int i = start + 1, j = end - 1, pivot = array[start];
        while (true) {
            while (i < end && array[i] <= pivot) {
                i++;
            }

            while (array[j] > pivot) {
                j--;
            }

            if (i >= j) {
                break;
            }

            swap(array, i, j);
        }

        if (j > start) {
            swap(array, start, j);
        }

        quickSort(array, start, j);
        quickSort(array, j + 1, end);
    }

    public int[] quickSort(int[] array) {
        quickSort(array, 0, array.length);
        return array;
    }
}
```
