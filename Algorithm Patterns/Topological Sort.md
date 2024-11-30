## Topological Sort 

The **Topological Sort Pattern** is a method used to process tasks or nodes in a specific order. This pattern is commonly applied to problems involving **dependency graphs**, where some tasks must be completed before others.

Imagine we’re organizing tasks for a project:
- Task A must be done before Task B.
- Task B must be done before Task C.

The **Topological Sort** helps us determine a valid order to complete these tasks while respecting the dependencies.

##### Key Concept:
Topological Sort works only on **Directed Acyclic Graphs (DAGs)**:
- **Directed**: Dependencies point in one direction (e.g., Task A → Task B).
- **Acyclic**: There are no cycles (e.g., A → B → A is not allowed).


#### Where is Topological Sort Useful?

We’ll use this pattern in scenarios like:
1. **Task scheduling**: Order tasks based on dependencies.
2. **Course prerequisites**: Determine the order to take courses.
3. **Build systems**: Figure out the order to compile files.


1. **Represent dependencies as a graph**:
   - Each task or node is a vertex.
   - Dependencies are directed edges between vertices.

2. **Track in-degrees**:
   - The **in-degree** of a node is the number of edges pointing to it.
   - Nodes with `in-degree = 0` have no dependencies and can be processed immediately.

3. **Process nodes in order**:
   - Start with nodes that have `in-degree = 0`.
   - Remove them from the graph and update the in-degrees of their neighbors.
   - Repeat until all nodes are processed.


#### Example Problem: Task Scheduling

##### Problem:
You have 6 tasks (`0` to `5`) and these dependencies:
```
0 → 1, 0 → 2, 1 → 3, 1 → 4, 2 → 4, 3 → 5, 4 → 5
```

Find a valid order to complete all tasks.

##### Approach:

1. Represent the tasks and dependencies as a graph:
   ```
   Graph:
   0 → 1, 0 → 2
   1 → 3, 1 → 4
   2 → 4
   3 → 5
   4 → 5
   ```

2. Calculate in-degrees for all nodes:
   ```
   In-degrees:
   0: 0
   1: 1
   2: 1
   3: 1
   4: 2
   5: 2
   ```

3. Start with nodes having `in-degree = 0` (like `0`), and process them one by one.

---

#### Code:
```python
def topological_sort(tasks, dependencies):
    # Step 1: Initialize graph and in-degrees
    graph = {i: [] for i in range(tasks)}
    in_degree = {i: 0 for i in range(tasks)}

    # Step 2: Build the graph
    for parent, child in dependencies:
        graph[parent].append(child)
        in_degree[child] += 1

    # Step 3: Find all nodes with in-degree = 0
    zero_in_degree = [node for node in in_degree if in_degree[node] == 0]

    result = []
    
    # Step 4: Process nodes with in-degree = 0
    while zero_in_degree:
        node = zero_in_degree.pop(0)  # Take one node with no dependencies
        result.append(node)

        # Reduce in-degree of neighbors
        for neighbor in graph[node]:
            in_degree[neighbor] -= 1
            if in_degree[neighbor] == 0:
                zero_in_degree.append(neighbor)

    # Step 5: If all nodes are processed, return the result
    if len(result) == tasks:
        return result
    else:
        return []  # Cycle detected, no valid ordering

# Example usage
tasks = 6
dependencies = [(0, 1), (0, 2), (1, 3), (1, 4), (2, 4), (3, 5), (4, 5)]
print("Topological Sort Order:", topological_sort(tasks, dependencies))
```

1. **Graph Representation**:
   ```
   0 → [1, 2]
   1 → [3, 4]
   2 → [4]
   3 → [5]
   4 → [5]
   ```

2. **In-Degrees**:
   ```
   0: 0
   1: 1
   2: 1
   3: 1
   4: 2
   5: 2
   ```

3. **Processing Nodes**:
   - Start with `0` (in-degree = 0).
   - Process `1` and `2` next.
   - Then `3` and `4`.
   - Finally, `5`.



##### Output:
For the above example:
```
Topological Sort Order: [0, 1, 2, 3, 4, 5]
```

---

### Real-Life Example:
Imagine planning a house construction:
- You need to lay the foundation before building walls.
- You need to finish walls before adding the roof.
- Topological Sort ensures you don’t try to install the roof before the foundation!

