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
