
In JavaScript, `var`, `let`, and `const` are used to declare variables, but they have some differences in terms of scope, hoisting, and mutability:

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
