
### Chapter 7 

#### Deep copy when dealing with unknown source

- **Focus**: Ensuring copy-on-write (COW) principles remain intact when integrating third-party or untrusted code.

- **Challenge**:
  - Our code handles data immutably.
  - External sources might still mutate this data, affecting our system.

- **Solution**: 
  - **Deep Copying (Defensive Copying)**:
    - Create a deep copy of all nested data.
    - Apply this when:
      - Receiving input from third-party sources.
      - Returning data to external functions.
    - Purpose: Ensure that any external mutations don’t affect our immutable code.



![image](https://github.com/user-attachments/assets/e1d8b9dd-73c1-4fa4-ae38-458cc7b30e43)


- **Considerations**:
  - **Deep Copying**:
    - Resource-intensive (duplicates all data structures).
  - **Shallow Copying**:
    - Copies only references, saving memory.
  - **Usage**:
    - Use deep copying selectively.
    - Best for dealing with unknown sources or functions to protect code immutability.

![image](https://github.com/user-attachments/assets/ab86d406-6dee-4885-9b5e-576e82fed953)


## Summary: 

This chapter is about keeping our copy-on-write (COW) approach intact when dealing with third-party or untrusted code. Even though our code handles data immutably, outside code might still change it and mess things up.

To prevent this, the chapter suggests using deep copying. This means making a full copy of all the data, both when we receive it and when we pass it on, to protect our code from any external changes.

But keep in mind, deep copying is heavy on resources since it duplicates everything. So, it's best to use it only when necessary, like when dealing with unknown sources, to keep our code safe.


