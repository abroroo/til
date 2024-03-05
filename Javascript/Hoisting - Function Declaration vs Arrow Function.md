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