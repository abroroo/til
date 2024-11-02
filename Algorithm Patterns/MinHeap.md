
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

