# Grokking Simplicity 

I'm reading a book that I find really useful, so I'm going to save my notes here as I go through the chapters.

## Part 1

## Chapter 1

Functional programming breaks down code into three main types: actions, calculations, and data. The goal is to reduce unexpected changes and make the code less dependent.

1. **Actions**: Functions that can give different results depending on when or how often you call them.
2. **Calculations**: Functions that always give the same result for the same input, no matter when you run them.
3. **Data**: Static information that doesn't change and can be used anywhere in the program.

The main idea of functional programming is to sort your code into these groups and try to turn actions into calculations, and calculations into data whenever possible. This helps cut down on unexpected changes and makes your code more reliable.

**Side effect**: Stuff that happens that isn't just the return value of a function.
