##### Get Keys In Binary Tree Layer By Layer
Get the list of list of keys in a given binary tree layer by layer. Each layer is represented by a list of keys and the keys are traversed from left to right.

**Examples**
```
        5
      /    \
    3        8
  /   \        \
1      4        11
```
the result is [[5], [3, 8], [1, 4, 11]]

**Corner Cases**

* What if the given binary tree is null? Return an empty list in this case.

**How is the binary tree represented?**

* We use the level order traversal sequence with a special symbol "#" denoting the null node.

**For Example:**

The sequence [1, 2, 3, #, #, 4] represents the following binary tree:
```
    1
  /   \
 2     3
      /
    4
```

**Answers**
**Analysis:**
a. what kind of data structure that this algorithm uses:
    Queue
b. what are actions of this algorithm step by step
    a. create a queue
    b. offer the root into queue
    c. while queue.size() > 0
        1. expand first element in the queue, put it in the current level list, current level count - 1
        2. put all generated children into queue, count with next level count

```java
/**
 * public class TreeNode {
 *   public int key;
 *   public TreeNode left;
 *   public TreeNode right;
 *   public TreeNode(int key) {
 *     this.key = key;
 *   }
 * }
 */
public class Solution {
    public List<List<Integer>> layerByLayer(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();

        if (root == null) {
            return result;
        }

        LinkedList<TreeNode> queue = new LinkedList<>();
        List<Integer> currLevel = new ArrayList<>();
        int currLevelCount = 1;
        int nextLevelCount = 0;

        queue.offer(root);

        while (queue.size() > 0) {
            TreeNode curr = queue.poll();
            currLevel.add(curr.key);
            currLevelCount--;

            if (curr.left != null) {
                queue.offer(curr.left);
                nextLevelCount++;
            }
            if (curr.right != null) {
                queue.offer(curr.right);
                nextLevelCount++;
            }
            if (currLevelCount == 0) {
                result.add(currLevel);
                currLevel = new ArrayList<>();
                currLevelCount = nextLevelCount;
                nextLevelCount = 0;
            }
        }

        return result;
    }
}
```
