### Heap Data Structure Overview

A **Heap** is a tree-based data structure that satisfies the **heap property**, which depends on the type of heap:

- **Min Heap**: Each parent node is smaller than or equal to its children.
- **Max Heap**: Each parent node is greater than or equal to its children.

### Heap as an Array and Tree Representation

Consider this array representation for a heap: **[18, 15, 12, 10, 5, 8, 3]**

Here’s the binary tree structure for this Max Heap example:

```
           18
         /    \
       15      12
      /   \    /   \
    10     5  8     3
```

#### Array Representation and Index Relationships
In array form, each element’s position is mapped to the tree structure by index formulas:

- **Root** is at index `0` (value `18`).
- **Left child** of index `i` is at index `2 * i + 1`
- **Right child** of index `i` is at index `2 * i + 2`
- **Parent** of index `i` is at `(i - 1) // 2`

#### Example of Relationships

1. **Root Node (18)**:
   - Index `0`
   - Left child at index `1` (value `15`)
   - Right child at index `2` (value `12`)

2. **Node (15)**:
   - Index `1`
   - Left child at index `3` (value `10`)
   - Right child at index `4` (value `5`)

3. **Node (12)**:
   - Index `2`
   - Left child at index `5` (value `8`)
   - Right child at index `6` (value `3`)

---

### Min Heap vs Max Heap

- **Min Heap**: Root holds the **smallest element**; each parent node is smaller than or equal to its children.
- **Max Heap**: Root holds the **largest element**; each parent node is greater than or equal to its children.

> The choice between Min and Max Heaps depends on your specific needs for prioritized access:
> - Use a **Min Heap** when you need quick access to the smallest element (e.g., scheduling, managing earliest times).
> - Use a **Max Heap** when you need quick access to the largest element (e.g., priority queues where highest priority tasks come first).

### Heap Operations

- **Insertion**: Add element to the end and **heapify up** to maintain the heap property.
- **Deletion**: Remove the root, replace with the last element, and **heapify down**.
- **Child Access**:
  - Left child: `2 * i + 1`
  - Right child: `2 * i + 2`
  - Parent: `(i - 1) // 2`

### Code Snippets

1. **Insertion** for Min Heap / Max Heap:

   ```python
   def insert(self, value):
       self.heap.append(value)
       self._heapify_up(len(self.heap) - 1)

   def _heapify_up(self, index):
       parent = (index - 1) // 2
       # Adjust comparison for Min or Max Heap by changing `<` to `>` as needed
       if index > 0 and self.heap[index] < self.heap[parent]:  # Min Heap condition
           self.heap[index], self.heap[parent] = self.heap[parent], self.heap[index]
           self._heapify_up(parent)
   ```

2. **Deletion** for Min Heap / Max Heap:

   ```python
   def remove(self):
       if not self.heap:
           return None
       root_value = self.heap[0]
       self.heap[0] = self.heap.pop()
       self._heapify_down(0)
       return root_value

   def _heapify_down(self, index):
       smallest = index  # For Min Heap, use smallest; for Max Heap, use largest
       left = 2 * index + 1
       right = 2 * index + 2

       if left < len(self.heap) and self.heap[left] < self.heap[smallest]:  # Min Heap condition
           smallest = left
       if right < len(self.heap) and self.heap[right] < self.heap[smallest]:  # Min Heap condition
           smallest = right

       if smallest != index:
           self.heap[index], self.heap[smallest] = self.heap[smallest], self.heap[index]
           self._heapify_down(smallest)
   ```

---

### Real World Usage Examples

#### When to Use Min Heaps
For managing resources that need **earliest availability**, like meeting rooms, CPU scheduling, or task prioritization.

1. **Quick Access to Smallest Element**: Root always holds the smallest element.
2. **Efficient Add and Remove**: Min Heap operations (insert and remove) are fast at `O(log N)`.
3. **Space Efficiency**: Requires `O(N)` space, storing only current end times or minimum values.

#### When to Use Max Heaps
Perfect for tracking **highest priorities**, such as implementing a **priority queue** where the task with the highest importance or urgency is handled first.

1. **Quick Access to Largest Element**: Root always holds the largest element.
2. **Efficient Add and Remove**: Max Heap operations (insert and remove) are both `O(log N)`.
3. **Space Efficiency**: Optimal space with `O(N)` complexity, storing only elements with priority.

