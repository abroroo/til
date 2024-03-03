# How to use useReducer?
Here's the basic syntax for useReducer:

```javascript

const [state, dispatch] = useReducer(reducer, initialState);
```

 - __`state`__: The current state value.
 - __`dispatch`__: A function used to dispatch actions to update the state.
 - __`reducer`__: A function that receives the current state and an action, and returns the new state based on the action.
 - __`initialState`__: The initial state value.

```javascript
import React, { useReducer } from 'react';

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
    </>
  );
}

export default Counter;

```
