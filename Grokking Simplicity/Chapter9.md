
# Chapter 9: Abstraction Barrier

### Abstraction Barrier

Another pattern in stratified design is the abstraction barrier. The idea is to wrap complex logic or language-specific code into separate functions, hiding the implementation details.

This way, you can ignore the programming language stuff and focus on your business or app logic.


![image](https://github.com/user-attachments/assets/f1adf1f7-7b3f-433d-b769-e348824a1431)


### Minimal Interface 

The minimal interface approach says that if you can implement a function in a higher layer using existing functions from the layer below, you should.

The idea is that once you’ve got your functions in place, they shouldn’t need to change or have new ones added later. Each layer should be complete and minimal, with functions that stand the test of time. That’s the goal of the minimal interface pattern—keeping everything straightforward and timeless.
 
