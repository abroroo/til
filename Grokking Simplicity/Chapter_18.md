# Chapter 18: Reactive and Onion Patterns

## Reactive Pattern

A **reactive architecture** is a design approach where systems automatically respond to changes or events in real time.

## When to Apply the Reactive Pattern

Use the reactive pattern when you have a state or value that, when it changes, triggers updates or calculations in other parts of the system.

You can implement this pattern using **Observer**, or libraries like **Recoil** or **Redux** in JavaScript.

### Example

You can create a primitive like `ValueCell`, where the central state (that many things depend on) is stored. This `ValueCell` has methods or **Observers** (watchers) that automatically trigger every time the state changes.

![image](https://github.com/user-attachments/assets/eef350e7-e61b-41b3-b903-28044cea734b)

![image](https://github.com/user-attachments/assets/dc004774-74e7-4ac7-b18d-e9b4e821e13a)



## Onion Architecture

**Onion Architecture** is a software design pattern that emphasizes keeping the core business logic (domain) independent from external concerns (like UI, databases, frameworks). 

### Key Concepts:
1. **Layers**: The architecture is structured in layers, forming a shape like an onion.
   - **Core/Domain Layer**: The innermost layer contains business logic, domain models, and rules. It has no dependencies on other layers.
   - **Application Layer**: Contains services and use cases that orchestrate domain models.
   - **Interface/Infrastructure Layer**: Handles external systems (databases, APIs, UI). This is the outermost layer, dependent on the core, but not vice versa.


### Example:
- The core contains your business rules (like a `Customer` entity and its operations).
- The outer layer could use an API or database to interact with the `Customer`, but the business rules don’t depend on how or where the data is stored.

![image](https://github.com/user-attachments/assets/6ecb1675-86f3-421a-b49f-8753da8868e8)


![image](https://github.com/user-attachments/assets/3407870c-6973-4450-ac77-6c7ba13d71ee)

