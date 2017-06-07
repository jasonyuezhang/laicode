##### Bipartite
Determine if an undirected graph is bipartite. A bipartite graph is one in which the nodes can be divided into two groups such that no nodes have direct edges to other nodes in the same group.

**Examples**
```
1 -- 2
   /
3 -- 4
```
is bipartite (1, 3 in group 1 and 2, 4 in group 2).
```
1 -- 2
   / |
3 -- 4
```
is not bipartite.

**Assumptions**
* The graph is represented by a list of nodes, and the list of nodes is not null.

**Answers**
**Assumptions**
The graph is represented by a list of nodes, and the list of nodes is not null.
**Analysis:**
a. what kind of data structure that this algorithm uses:
    FIFO Queue, HashMap 
b. what are actions of this algorithm step by step (BFS)
    a. maintain a FIFO queue
    b. offer the start node into queue
    c. while queue.size() > 0
        1. expand the first node in the queue, put it into HashMap with correct group value. If the node is visited with different group value, return false
        2. put all generated node into queue
    d. if all element expanded correctly, return true.

```java
/**
 * public class GraphNode {
 *   public int key;
 *   public List<GraphNode> neighbors;
 *   public GraphNode(int key) {
 *     this.key = key;
 *     this.neighbors = new ArrayList<GraphNode>();
 *   }
 * }
 */
public class Solution {
    public boolean isBipartite(List<GraphNode> graph) {
        // null check
        if (graph == null) {
            return true;
        }

        LinkedList<GraphNode> queue = new LinkedList<>();
        HashMap<GraphNode, Integer> map = new HashMap<>();
        int currGroup = 1;

        queue.offer(graph.get(0));
        map.put(graph.get(0), 0);
        
        while (queue.size() > 0) {
            GraphNode curr = queue.poll();
            for (GraphNode adj : curr.neighbors) {
                if (map.containsKey(adj)) {
                    if (map.get(adj) != currGroup) {
                        return false;    
                    } else {
                        continue;
                    }
                }
                queue.offer(adj);
                map.put(adj, currGroup);
            }
            currGroup ^= 1;
        }

        return true;
    }
}
```
