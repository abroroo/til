# Grokking Simplicity 

This is a book I've found useful to read, so as I read thorugh the chapters, I'll save my notes in here 

## Part 1

## Chapter 1

Functional programming categorizes code into three main categories: actions, calculations, and data, aiming to minimize side effects and enhance code robustness.

1. **Actions**: These are functions whose outputs depend on when or how many times they are called, potentially yielding different results each time.
2. **Calculations**: Inert functions that consistently produce the same output for the same input, regardless of when they are executed.
3. **Data**: Static information that remains unchanged and can be accessed uniformly throughout the program.

The core principle of functional programming involves categorizing code into these groups and transforming actions into calculations and calculations into data where feasible. This approach helps mitigate unforeseen side effects, thereby enhancing application robustness.

**Side effect**: Things that happen that are not defined by return value.
