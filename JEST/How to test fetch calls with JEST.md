## How to test fetch APIs with JEST 


Some common scenarios for asynchronous testing:

1. #### Callback Functions:
  - Functions that use callbacks.
  - Functions that use setTimeout.
    
2. #### Promises:
  - Functions that return promises.
  - API calls.
3. ##### Async/Await:
  - Modern syntax for handling promises.


Let's take a look at each scenario and how to test it using Jest. 

## Callback Functions:

Consider a simple function that takes a callback and executes it after a delay:

<img src="https://raw.githubusercontent.com/abroroo/til/main/JEST/images/1.png" width="500" height="300" />

And a test for this function:

<img src="https://raw.githubusercontent.com/abroroo/til/main/JEST/images/1.2.png" width="800" height="270" />

## Promises:

Consider a function that returns a Promise

<img src="https://raw.githubusercontent.com/abroroo/til/main/JEST/images/2.png" width="500" height="300" />

And a test for this function:

<img src="https://raw.githubusercontent.com/abroroo/til/main/JEST/images/2.1.png" width="700" height="200" />

## Async/Await:

The same aboove mentioned promise-based function can be tested using async/await too: 

<img src="https://raw.githubusercontent.com/abroroo/til/main/JEST/images/2.2.png" width="900" height="200" />
