I am sure you've used or heard of `bind`, `call`, and `apply` built in Javascript. 

Here I just tried to consicely write about each, so I can refer to it whenever I need to. 

# When to use: 
There methods are useful when you want to reuse a function in different contexts or with different sets of arguments, without having to modify the function itself.

# How to use:

## 1. __`bind`__: 
   The `bind` method creates a new function that, when called, has its `this` value set to the provided value.
   
   It allows you to create a new function with a specific `this` value and optionally pass in some initial arguments.

   ```javascript
    const person = {
      name: 'John',
      greet: function() {
        console.log(`Hello, my name is ${this.name}`);
      }
    }
    
    const boundGreet = person.greet.bind({ name: 'Jane' });
    boundGreet(); // Output: Hello, my name is Jane
   ```
   In the example above, `bind` creates a new function `boundGreet` that, when called, will have its this value set to `{ name: 'Jane' }`. This is useful when you want to ensure that a function is called with a specific context (`this` value).

## 2. __`call`__: 

   The `call` method calls a function with a given this value and arguments provided individually.

   ```javascript
   const person = {
     name: 'John',
     greet: function(greeting, punctuation) {
       console.log(`${greeting}, my name is ${this.name}${punctuation}`);
     }
   }
   
   person.greet.call({ name: 'Jane' }, 'Hi', '!'); // Output: Hi, my name is Jane!
   ```
   In this example, `call` is used to invoke the `greet` function with `{ name: 'Jane' }` as the this value, and `'Hi'` and `'!'` as the arguments.

## 3. __`apply`__: 

   The `apply` method is similar to `call`, but it __takes the arguments as an array instead of individual values__.

   ```javascript
   const person = {
     name: 'John',
     greet: function(greeting, punctuation) {
       console.log(`${greeting}, my name is ${this.name}${punctuation}`);
     }
   }
   
   person.greet.apply({ name: 'Jane' }, ['Hello', '?']); // Output: Hello, my name is Jane?
   ```
   Here, `apply` invokes the `greet` function with `{ name: 'Jane' }` as the `this` value, and the arguments `['Hello', '?']` are passed as an array.
   
