Javascript has some bahavior called [Hoisting](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting) 

Consider this two examples 

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
and this is called hoisting, Hoisting is a JavaScript mechanism where variables and function declarations are moved to the top of their containing scope during the compile phase before the code execution
