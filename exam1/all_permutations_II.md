##### All Permutations II

Given a string with possible duplicate characters, return a list with all permutations of the characters.

**Examples**

* Set = “abc”, all permutations are [“abc”, “acb”, “bac”, “bca”, “cab”, “cba”]
* Set = "aba", all permutations are ["aab", "aba", "baa"]
* Set = "", all permutations are [""]
* Set = null, all permutations are []

```java
public class Solution {
    public List<String> permutations(String set) {
        List<String> result = new List<>();

        if (set == null) {
            return result;
        }
        // Write your solution here.
        return permutations(set.toCharArray(), 0, result);
    }

    public List<String> permutations(char[] set, int level, List<String> result) {
        if (set.length == 0) {
            result.add("");
            return result;
        } else if (set.length == level) {

        }



        return result;
    }
}
```

              ""
            / |   \
           a  b    c
       /|    /\    | \
    ab  ac  ba bc  ca cb
    
