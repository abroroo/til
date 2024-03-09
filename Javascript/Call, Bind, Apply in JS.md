I am sure you've used or heard of `bind`, `call`, and `apply` built in JS methods. 

Here I just tried to consicely write about each, so I can refer to it whenever I need to. 

1. __`bind`__: The `bind` method creates a new function that, when called, has its `this` value set to the provided value.
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

2. 
   
