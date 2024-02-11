[Selectors](https://recoiljs.org/docs/basic-tutorial/selectors) concept which by far is just like reducers in Redux 

Selectors in Recoil are primarily used to compute derived state based on the current state of atoms. They are pure functions that take the current state as input and return a new value based on that state.

### Key Concepts:
 - __Derived State__:

    Selectors compute derived state based on the values of one or more atoms. This derived state can represent complex data transformations, filtering, sorting, or any other computation based on the current state of the application.

- __Dependency Tracking__:

    Recoil automatically tracks dependencies between atoms and selectors. If a selector depends on an atom, Recoil will ensure that the selector is re-evaluated whenever the atom's value changes. This ensures that derived state stays in sync with the underlying atoms.

- __Immutability__:

    Selectors are pure functions, meaning they don't mutate state or have side effects. They take the current state as input and return a new value based on that state. This ensures that selectors are predictable and easy to reason about.


### Code Example:
Example of a todo list application

```javascript
import { atom, selector } from 'recoil';

// Atom for storing list of todos
export const todoListState = atom({
  key: 'todoListState',
  default: [],
  completed: false
});

// Selector to compute completed todos count
export const completedTodosCountSelector = selector({
  key: 'completedTodosCountSelector',
  get: ({ get }) => {
    const todoList = get(todoListState);
    return todoList.filter(todo => todo.completed).length;
  },
});

```
  - We define an atom __todoListState__ to store the list of todos.
  - We define a selector __completedTodosCountSelector__ to compute the count of completed todos based on the current state of todoListState.
The get function inside the selector retrieves the current value of todoListState using get(todoListState), filters the todos to get completed ones, and returns the count of completed todos.
