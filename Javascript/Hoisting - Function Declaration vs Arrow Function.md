Javascript has some bahavior called [Hoisting](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting) 

Consider these two examples 

1. 
```javascript
console.log(x); // undefined
var x = 10;

```
2. 
```javascript
console.log(y); // ReferenceError: y is not defined
y = 20;
```
First example is compiled as:
```javascript
var x;
console.log(x); // undefined
x = 10;
```
and this is called __hoisting__. Hoisting is a JavaScript mechanism where variables and function declarations are moved to the top of their containing scope during the compile phase before the code execution.

The reason you get a `ReferenceError` in the second example is that the variable `y` is not declared (no variable declaration part) before it's used.


# Now how does that affect functions? 

Well Javascript aplies hoisting only to function declaration using `function someFunc()` keyword, it doesn't apply hoisting to an arrow function `const someFunc => {}`. 

When you declare a function using the function keyword, the entire function declaration is hoisted to the top of its containing scope. This means that you can call the function before it appears in the code, and JavaScript will still recognize and execute it.

For Example:
```javascript
sayHello(); // Output: "Hello, world!"

function sayHello() {
  console.log("Hello, world!");
}

```

However, arrow functions are not hoisted in the same manner.

For Example:
```javascript
sayHello(); // This will result in a TypeError: sayHello is not a function

const sayHello = () => {
  console.log('Hello');
};

```
In this case, if you try to call `sayHello()` before it's defined, you'll encounter a TypeError because sayHello is not yet a function.

Arrow functions are typically used as expressions and are assigned to variables or passed as arguments to other functions. Since variable declarations are hoisted but not their assignments, if you try to use an arrow function before its declaration, you'll encounter an error.
