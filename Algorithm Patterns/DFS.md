## Depth-First Search (DFS) 

DFS is a method to explore or search through a tree or graph **by diving as deep as possible into one branch before backtracking**. It’s like exploring a maze by walking straight until you hit a wall, then retracing your steps to explore other paths.

1. Start at the root (or starting node).  
2. Visit one child node, then that child’s child, and so on until there are no more children.  
3. When you hit a dead end, **backtrack** to the most recent fork to explore unexplored paths.  


### Key Points to Remember  

1. **Recursive or Iterative:**  
   DFS can be implemented using recursion or an explicit stack. Both simulate backtracking.  

2. **Traversal Order Depends on Input:**  
   If nodes have children, DFS processes them in the order they appear in the data structure.  

3. **Great for Finding Paths:**  
   DFS is ideal when you want to explore all paths or detect cycles in a graph.  

### Input: Graph Representation  

DFS works on graphs or trees. These are often represented as dictionaries in Python:  

- **Graph Example:**  
  ```python
  graph = {
      'A': ['B', 'C'],
      'B': ['D', 'E'],
      'C': ['F'],
      'D': [],
      'E': [],
      'F': []
  }
  ```

---

### Recursive DFS Implementation  

```python
def dfs_recursive(graph, node, visited=None):
    if visited is None:
        visited = set()  # Set to track visited nodes

    visited.add(node)  # Mark the node as visited
    print(node, end=" ")  # Process the node (e.g., print it)

    for neighbor in graph[node]:  # Visit each neighbor
        if neighbor not in visited:
            dfs_recursive(graph, neighbor, visited)

# Example Usage
graph = {
    'A': ['B', 'C'],
    'B': ['D', 'E'],
    'C': ['F'],
    'D': [],
    'E': [],
    'F': []
}
print("Recursive DFS:")
dfs_recursive(graph, 'A')  # Output: A B D E C F
```

### Iterative DFS Implementation  

```python
def dfs_iterative(graph, start):
    visited = set()  # Set to track visited nodes
    stack = [start]  # Stack for DFS traversal

    while stack:
        node = stack.pop()  # Pop the top node (LIFO)
        if node not in visited:
            visited.add(node)  # Mark as visited
            print(node, end=" ")  # Process the node

            # Add neighbors in the order they appear in the graph
            for neighbor in graph[node]:
                if neighbor not in visited:
                    stack.append(neighbor)

# Example Usage
print("\nIterative DFS:")
dfs_iterative(graph, 'A')  # Output: A B D E C F
```


### Step-by-Step Walkthrough (Iterative DFS Example)  

Graph:  
```plaintext
       A
      / \
     B   C
    / \
   D   E
        \
         F
```

**Traversal Process:**  

| **Step** | **Stack**       | **Visited**         | **Current Node** | **Action**              |
|----------|-----------------|---------------------|------------------|-------------------------|
| 1        | `['A']`         | `{}`                | `A`              | Visit `A`, add `['B', 'C']`. |
| 2        | `['B', 'C']`    | `{A}`               | `C`              | Visit `C`.                  |
| 3        | `['B']`         | `{A, C}`            | `B`              | Visit `B`, add `['D', 'E']`. |
| 4        | `['D', 'E']`    | `{A, C, B}`         | `E`              | Visit `E`, add `['F']`.      |
| 5        | `['D', 'F']`    | `{A, C, B, E}`      | `F`              | Visit `F`.                  |
| 6        | `['D']`         | `{A, C, B, E, F}`   | `D`              | Visit `D`.                  |
| 7        | `[]`            | `{A, C, B, E, F, D}`| -                | Traversal complete.         |

---

### When to Use DFS  

1. **Pathfinding:**  
   - Useful to find a path between two nodes.  
   - Example: Does a route exist from A to E?  

2. **Cycle Detection:**  
   - Detect cycles in graphs (e.g., dependency problems).  

3. **Explore All Paths:**  
   - Ideal for finding **all solutions** in decision trees (e.g., maze solving).  

4. **Tree Traversals:**  
   - Preorder, Inorder, and Postorder traversals of a binary tree.  

---

- DFS is about exploring **deeply**, one branch at a time.  
- **Recursive DFS** is simpler but can risk stack overflow for large graphs.  
- **Iterative DFS** uses an explicit stack and is safer for large inputs.  
- Always track visited nodes to avoid infinite loops in cyclic graphs.  
