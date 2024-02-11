The Essense of Redux 


```javascript

// Define Actions
const increment = () => ({ type: 'INCREMENT' });
const decrement = () => ({ type: 'DECREMENT' });

// Define Reducer
const counterReducer = (state = 0, action) => {
  switch (action.type) {
    case 'INCREMENT':
      return state + 1;
    case 'DECREMENT':
      return state - 1;
    default:
      return state;
  }
};

// Create Store
const { createStore } = Redux;
const store = createStore(counterReducer);

// Dispatch Actions
store.dispatch(increment());
store.dispatch(increment());
store.dispatch(decrement());

// Subscribe to State Changes
store.subscribe(() => {
  console.log('Current Count:', store.getState());
});

```