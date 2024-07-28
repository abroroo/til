# Chapter 6

### Copy-on-Write (COW) in Functional Programming:

1. **Immutable Data Structures**: In functional programming, data structures are often immutable, meaning they cannot be changed once created. Instead of modifying an existing structure, you create a new one with the desired changes.

2. **Efficient Copying**: Copying large data structures can be expensive in terms of memory and time. COW optimizes this process by delaying the actual copying until it’s absolutely necessary.

3. **Shared Data**: When you "copy" a data structure using COW, the new structure initially shares the same data as the original. No actual copying happens at this point; both structures point to the same underlying data.

4. **Writing Changes**: When you need to modify the data, only the parts of the data structure that are being changed are copied. This is when the "write" part of COW happens. The rest of the data remains shared between the original and the new structure.

### Example:

Imagine you have a list [1, 2, 3] and you want to create a new list by changing the last element to 4.

- **Original List**: [1, 2, 3]
- **New List**: [1, 2, 4]

With COW:
1. **Initial Copy**: The new list points to the same elements as the original list: [1, 2, 3]. No data is copied yet.
2. **Modification**: When you change the last element, only the part of the list that is modified (the last element) is copied.
3. **Result**: The new list [1, 2, 4] shares the first two elements with the original list, and only the last element is a new copy.

### Benefits:

- **Memory Efficiency**: Saves memory by sharing unchanged parts of data structures.
- **Performance**: Improves performance by avoiding unnecessary copying.




![image](https://github.com/user-attachments/assets/2bd80468-c4ea-4881-86a1-a63f2f9759c2)

- You can convert actions into calculation just by copying an input data and modifying that copied data and return copied data leaving original data immutable. Which overall makes it a read operation, because the original data hasn't been modified.
- One the clean code pattern is to calcualtion function to copy the input and then modify , instead of creatinga copy in the parent function and then passing that newly created copy as input to the calculation.

![image](https://github.com/user-attachments/assets/0de44c95-d8e1-415c-88cc-5f05af16e88e)


### Immutable data:
![image](https://github.com/user-attachments/assets/d3b61d8c-85e8-4ff4-a33b-f7c70e910d46)
 
