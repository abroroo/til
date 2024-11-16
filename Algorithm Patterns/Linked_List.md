## Linked List
A **linked list** is a data structure that consists of a sequence of elements, where each element (called a **node**) points to the next one in the sequence. 

```
[Head | Node 1] -> [Node 2] -> [Node 3] -> [Node 4] -> [Tail | Node 5] -> None
```

Unlike arrays, linked lists don't store elements in contiguous memory locations, which means: 
> In an **array**, elements are stored next to each other in a block of memory, so if you want to add more items than the array can hold, you might need to create a new, larger array and copy everything over. This takes time and space.

> In a **linked list**, each item (node) is stored separately in memory, and each node just points to the next one. This means you can easily add or remove items without needing to move or copy other elements, making linked lists great when you need flexible, dynamic data sizes that can grow or shrink without hassle.


- **Node Structure**: Each node has:
  - **Value**: The data stored in the node.
  - **Next Pointer**: A reference (or link) to the next node in the list.
- **Head**: The first node in the list.
- **Tail**: The last node, which points to `null` (or `None` in Python), indicating the end of the list.

### Reversing a Linked List In-Place
To reverse a linked list in place, you need to change the direction of the `next` pointers of each node. This makes the list go backward without creating a new list or using extra space.

Here's a step-by-step way to think about it:

1. **Initialize Pointers**:
   - `prev` starts as `None` (to mark the new end of the list).
   - `current` starts at the `head` (the current node you're processing).

2. **Iterate Through the List**:
   - Save the `next` node temporarily so you don’t lose the rest of the list.
   - Change the `next` pointer of `current` to point to `prev`.
   - Move `prev` to `current` and `current` to `next`.
   - Repeat until `current` becomes `None` (end of the list).

3. **Update the Head**:
   - Set `head` to `prev` because `prev` is now the first node of the reversed list.

### Simple Python Code:
Here's how you can reverse a linked list in Python:

```python
class ListNode:
    def __init__(self, value=0, next=None):
        self.value = value
        self.next = next

def reverse_linked_list(head):
    prev = None
    current = head
    
    while current:
        next_node = current.next  # Save the next node
        current.next = prev       # Reverse the current node's pointer
        prev = current            # Move prev to current
        current = next_node       # Move current to next
    
    return prev  # New head of the reversed list
```

### Visualization:
If you have a linked list like this:
```
1 -> 2 -> 3 -> 4 -> None
```

After reversing, it becomes:
```
4 -> 3 -> 2 -> 1 -> None
```

The `head` now points to `4`, and each node's `next` points in the opposite direction compared to the original list.


![image](https://github.com/user-attachments/assets/1943a012-9940-49c1-8450-fc82f8665998)


