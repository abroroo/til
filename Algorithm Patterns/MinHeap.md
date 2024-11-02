
### Min Heap Tree Example

Consider a Min Heap represented as an array: **[3, 5, 8, 10, 15, 12, 18]**

This Min Heap follows the rule that each parent node is smaller than or equal to its children. Here's how it looks as a binary tree:

```
           3
         /   \
       5       8
     /   \    /   \
   10   15  12   18
```

#### Array Representation and Index Relationships
In array form, each element’s position is mapped directly to the tree structure by index formulas:

- **Root** is at index `0` (value `3`).
- **Left child** of index `i` is at index `2 * i + 1`
- **Right child** of index `i` is at index `2 * i + 2`
- **Parent** of index `i` is at `(i - 1) // 2`

#### Example of Relationships

1. **Root Node (3)**:
   - Index `0`
   - Left child at index `1` (value `5`)
   - Right child at index `2` (value `8`)

2. **Node (5)**:
   - Index `1`
   - Left child at index `3` (value `10`)
   - Right child at index `4` (value `15`)

3. **Node (8)**:
   - Index `2`
   - Left child at index `5` (value `12`)
   - Right child at index `6` (value `18`)

### Key Points
- The **smallest element** is always at the root.
- Each parent node is smaller than or equal to its children, preserving the Min Heap property.
- The Min Heap structure is **complete** (filled left to right), which ensures efficient insertion and deletion. 





---

#### Min Heap Basic operations
- **Insertion**: Add element to the end and **heapify up** to maintain Min Heap property.
- **Deletion**: Remove the root, replace with last element, and **heapify down**.
- **Child Access**:
  - Left child: `2 * i + 1`
  - Right child: `2 * i + 2`
  - Parent: `(i - 1) // 2`

#### Code Snippets

1. **Insertion**: Adds to end of array, then fixes Min Heap property by moving element up.

   ```python
   def insert(self, value):
       self.heap.append(value)
       self._heapify_up(len(self.heap) - 1)

   def _heapify_up(self, index):
       parent = (index - 1) // 2
       if index > 0 and self.heap[index] < self.heap[parent]:
           self.heap[index], self.heap[parent] = self.heap[parent], self.heap[index]
           self._heapify_up(parent)
   ```

2. **Deletion**: Removes the root (minimum element), replaces it with last element, and restores heap property by moving it down.

   ```python
   def remove_min(self):
       if not self.heap:
           return None
       min_value = self.heap[0]
       self.heap[0] = self.heap.pop()
       self._heapify_down(0)
       return min_value

   def _heapify_down(self, index):
       smallest = index
       left = 2 * index + 1
       right = 2 * index + 2

       if left < len(self.heap) and self.heap[left] < self.heap[smallest]:
           smallest = left
       if right < len(self.heap) and self.heap[right] < self.heap[smallest]:
           smallest = right

       if smallest != index:
           self.heap[index], self.heap[smallest] = self.heap[smallest], self.heap[index]
           self._heapify_down(smallest)
   ```

3. **Accessing Children and Parent**:

   ```python
   # For node at index i:
   left_child = 2 * i + 1
   right_child = 2 * i + 2
   parent = (i - 1) // 2
   ```

#### Summary

- **Heapify Up**: Used after **insertion** to move the new element up until the Min Heap property is satisfied.
- **Heapify Down**: Used after **deletion** to move the root element down, restoring the Min Heap property by swapping with the smaller child when necessary.
- **Array Representation**: Keep elements in an array and use indexing formulas to access children and parent nodes directly.

