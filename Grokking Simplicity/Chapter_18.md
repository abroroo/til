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


