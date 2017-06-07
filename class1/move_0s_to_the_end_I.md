##### Move 0s to the end
**Assumptions:**
* The given array is not null.

**Examples:**
* {1} --> {1}
* {1, 0, 3, 0, 1} --> {1, 3, 1, 0, 0} or {1, 1, 3, 0, 0} or {3, 1, 1, 0, 0}

```java
public class Solution {
    // swap to elements in array
    private void swap(int[] array, int i, int j) {
        int tmp = array[i];
        array[i] = array[j];
        array[j] = tmp;
    }

    public int[] moveZero(int[] array) {
        int i = 0, j = array.length - 1;
        while (i <= j) {
            if (array[i] == 0) {
                swap(array, i, j);
                j--;
            } else {
                i++;
            }
        }

        return array;
    } 
}
```
