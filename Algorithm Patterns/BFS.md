
## BFS (Breadth-First Search)

BFS is a way to explore or search through a tree or graph **one level at a time**, starting from the top.  

Think of it like this:
1. Start with the first level (the root or starting node).
2. Then move to the second level (its direct children).
3. Keep going deeper, level by level, until all nodes are visited or you find what you’re looking for.

**Analogy:** Imagine exploring all the rooms on the first floor of a building before moving to the second floor, then the third, and so on.


#### How BFS Works:
1. Use a **queue** (helps to visit items in order).
2. Start by adding the first node to the queue.
3. While the queue isn’t empty:
   - Remove the first node (FIFO: First In, First Out).
   - Process it (e.g., check if it’s your target).
   - Add its **children or neighbors** to the queue.
4. Repeat until you find your target or the queue is empty.


#### BFS for Arrays
Sometimes, input data is an array but can be visualized as a binary tree:
- The first element (`index 0`) is the **root**.
- For an element at index `i`:
  - **Left child:** `2*i + 1`
  - **Right child:** `2*i + 2`


### BFS Example 1: Search in an Array (as a Tree)
```python
def bfs_search_array_tree(arr, target):
    n = len(arr)
    queue = [0]  # Start at the root (index 0)

    while queue:
        idx = queue.pop(0)
        
        if arr[idx] == target:
            return f"Found {target} at index {idx}!"
        
        # Add children to the queue
        left, right = 2 * idx + 1, 2 * idx + 2
        if left < n:
            queue.append(left)
        if right < n:
            queue.append(right)

    return f"{target} not found."

# Example
arr = [1, 2, 3, 4, 5, 6]
print(bfs_search_array_tree(arr, 5))  # Found 5 at index 4
print(bfs_search_array_tree(arr, 7))  # 7 not found
```

---

### BFS Example 2: Shortest Path in a Graph
```python
from collections import deque

def bfs_shortest_path(graph, start, target):
    queue = deque([(start, [start])])
    visited = set()

    while queue:
        current, path = queue.popleft()
        if current == target:
            return path

        visited.add(current)
        for neighbor in graph[current]:
            if neighbor not in visited:
                queue.append((neighbor, path + [neighbor]))

    return None

# Example Graph
graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D', 'E'],
    'C': ['A'],
    'D': ['B'],
    'E': ['B']
}

# Find shortest path
print(bfs_shortest_path(graph, 'A', 'E'))  # ['A', 'B', 'E']
```

```markdown
            A
           / \
          B   C
         / \
        D   E


```
---

### When to Use BFS
1. **Shortest Path Problems:** Unweighted graphs or grids.
   - Example: "Find the minimum steps to reach a target."
2. **Level-by-Level Processing:** Trees or hierarchical data.
   - Example: "Return values at each level of a binary tree."
3. **Exploring Regions:** Problems like connected components or "flood fill."
   - Example: "Count islands in a grid."

### Complexity of BFS
- **Time Complexity:** O(V + E)  
  (Visit each node and edge once.)
- **Space Complexity:** O(V)  
  (The queue may hold all nodes of the largest level.)

