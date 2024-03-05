
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
