
In JavaScript, `var`, `let`, and `const` are used to declare variables, but they have some differences in terms of scope, hoisting, and mutability:

If you are not familiar with hoisting, I've covered it a little bit in [here](https://github.com/abroroo/til/blob/main/Javascript/Hoisting%20-%20Function%20Declaration%20vs%20Arrow%20Function.md)

__`var`__:

 - `var` declarations are function-scoped or globally scoped, but not block-scoped.
 - Variables declared with var are hoisted to the top of their scope and initialized with undefined.
 - They can be re-declared and updated within their scope.
 - Example:
     ```javaScript
     function example() {
       if (true) {
         var x = 10;
       }
       console.log(x); // 10
     }
     
     ```
__`let`__:

 - `let` declarations are block-scoped, meaning they are only accessible within the block they are declared in (like if, for, or while blocks).
 - Variables declared with let are hoisted to the top of their block but are not initialized.
 - They cannot be re-declared within the same block scope, but their values can be updated.
 - Example:
    ```javascript
    function example() {
      if (true) {
        let y = 20;
      }
      console.log(y); // ReferenceError: y is not defined
    }
    ```
__`const`__:

 - `const` declarations are also block-scoped.
 - Variables declared with const must be initialized during declaration, and their value cannot be changed once initialized.
 - Like let, variables declared with const are not hoisted to the top of their block.
 - Example:
