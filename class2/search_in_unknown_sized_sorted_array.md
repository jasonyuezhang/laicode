##### Search In Unknown Sized Sorted Array
Given a integer dictionary A of unknown size, where the numbers in the dictionary are sorted in ascending order, determine if a given target integer T is in the dictionary. Return the index of T in A, return -1 if T is not in A.

**Assumptions**
* dictionary A is not null
* dictionary.get(i) will return null if index i is out of bounds

**Examples**
* A = {1, 2, 5, 9, ......}, T = 5, return 2
* A = {1, 2, 5, 9, 12, ......}, T = 7, return -1

```java
/*
*  interface Dictionary {
*    public Integer get(int index);
*  }
*/

// You do not need to implement the Dictionary interface.
// You can use it directly, the implementation is provided when testing your solution.
public class Solution {
    public int search(Dictionary dict, int target) {
        if (dict.get(0) == null) {
            return -1;
        }

        int i = 1;
        int iPrev = 0;

        for (i = 1; dict.get(i) != null && target > dict.get(i); i *= 2) {
            iPrev = i;
        }

        int start = iPrev;
        int end = i;
        int mid = (start + end) / 2;

        while (start <= end) {
            if (dict.get(mid) == null) {
                end = mid - 1;
            } else if (target == dict.get(mid)) {
                return mid;
            } else if (target < dict.get(mid)) {
                end = mid - 1;
            } else {
                start = mid + 1;
            }
            mid = (start + end) / 2;
        }

        return -1;
    }
}
```
