##### Rainbow Sort
```java
public class Solution {
    private void swap (int[] array, int i, int j) {
        int tmp = array[i];
        array[i] = array[j];
        array[j] = tmp;
    }

    public int[] rainbowSort (int[] array) {
        int i = 0, j = array.length - 1, k = 0;

        while (k <= j) {
            if (array[k] < 0) {
                swap(array, k, i);
                i++;
                k++;
            } else if (array[k] > 0) {
                swap(array, k, j);
                j--;
            } else {
                k++;
            }
        }

        return array;
    }
}
```
