##### a to the power of b
**Examples**
* power(2, 0) = 1
* power(2, 3) = 8
* power(0, 10) = 0
* power(-2, 5) = -32

**Corner Cases**
* What if the result is overflowed? We can assume the result will not be overflowed when we solve this problem on this online judge.
```java
public class Solution {
    public long power(int a, int b) {
        // base cases
        if (b == 0) {
            return 1;
        }

        long value = power(a, b/2);

        value *= value;
        if ((b & 1) == 1) {
            value *= a;
        }

        return value;
    }
}
```
