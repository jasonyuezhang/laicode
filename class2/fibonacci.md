##### Fibonacci Number
**Examples**
* 0th fibonacci number is 0
* 1st fibonacci number is 1
* 2nd fibonacci number is 1
* 3rd fibonacci number is 2
* 6th fibonacci number is 8

**Corner Cases**
* What if K < 0? in this case, we should always return 0.
* Is it possible the result fibonacci number is overflowed? We can assume it will not be overflowed when we solve this problem on this online judge, but we should also know that it is possible to get an overflowed number, and sometimes we will need to use something like BigInteger.
```java
import java.util.HashMap;

public class Solution {
    HashMap<Integer, Long> cache = new HashMap<Integer, Long>();

    Solution () {
        cache.put(0, Long.valueOf(0));
        cache.put(1, Long.valueOf(1));
    }

    public long fibonacci(int K) {
        // negative check
        if (K < 0) {
            return 0;
        }

        // check if exist in cache
        if (cache.containsKey(K)) {
            return cache.get(K);
        }

        Long value = (Long)(fibonacci(K - 1) + fibonacci(K - 2));
        cache.set(K, value);

        return value;
    }
}
```
