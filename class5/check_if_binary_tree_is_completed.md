##### Check If Binary Tree is Completed
Check if a given binary tree is completed. A complete binary tree is one in which every level of the binary tree is completely filled except possibly the last level. Furthermore, all nodes are as far left as possible.

**Examples**
```
        5
      /    \
    3        8
  /   \
1      4
```
is completed.
```
        5
      /    \
    3        8
  /   \        \
1      4        11
```
is not completed.

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
**Assumptions**
The algorithm is runing against a binary tree and all element are integer
**Analysis:**
a. what kind of data structure that this algorithm uses:
    Queue
b. what are actions of this algorithm step by step
    a. create a queue
    b. offer the root into queue
    c. while queue.size() > 0
        1. take out the top element from queue and expand it
        2. add it's left child and right child into queue.
           ** If left is null, left and all the following generated children should be null as well, otherwise the tree is not completed.
           ** If right is null, all the following generated children should be null as well, otherwise the tree is nt completed.
    d. if all elements following above rules, the tree is completed.

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
    public boolean isCompleted(TreeNode root) {
        // null check
        if (root == null) {
            return true;
        }
        
        LinkedList<TreeNode> queue = new LinkedList<>();
        boolean hasNullChild = false;
        queue.offer(root);

        while (queue.size() > 0) {
            TreeNode curr = queue.poll();
            if (curr.left == null && curr.right == null) {
                hasNullChild = true;
                continue;
            }

            // check left child
            if (curr.left == null) {
                hasNullChild = true;
            } else if (hasNullChild) {
                return false;
            } else {
                queue.offer(curr.left);
            }

            // check right child
            if (curr.right == null) {
                hasNullChild = true;
            } else if (hasNullChild) {
                return false;
            } else {
                queue.offer(curr.right);
            }
        }

        return true;
    }
}
```
