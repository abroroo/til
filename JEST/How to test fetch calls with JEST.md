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


Let's go through each scenario.

### Callback Functions:

Consider a simple function that takes a callback and executes it after a delay:
```
// asyncFunc.js
function fetchData(callback) {
  setTimeout(() => {
    const data = 'Async Data';
    callback(data);
  }, 1000);
}

module.exports = { fetchData };

```
And a test for this function:
```
// asyncFunc.test.js
const { fetchData } = require('./asyncFunctions');

test('fetchData calls callback with correct data', (done) => {
  function callback(data) {
    expect(data).toBe('Async Data');
    done(); // This informs Jest that the asynchronous operation is complete.
  }

  fetchData(callback);
});

```
