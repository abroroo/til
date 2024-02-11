# How Selectors work in Recoil:

[Selectors](https://recoiljs.org/docs/basic-tutorial/selectors) in Recoil are kinda like reducers in Redux, but simpler

Selectors in Recoil are primarily used to compute derived state based on the current state of atoms. They're basically just functions that take the current state as input and give you back a new value based on that.

## Key Ideas:

 - __Derived State__:

   Selectors calculate new state by looking at what's in the atoms. This can be anything from doing math with numbers to filtering or sorting lists.

- __Dependency Tracking__:

    Recoil automatically tracks dependencies between atoms and selectors. If a selector depends on an atom, Recoil will ensure that the selector is re-evaluated whenever the atom's value changes. This way, everything stays in sync.

- __Immutability__:

    Selectors are pure functions, meaning they don't mutate state or have side effects. They take the current state as input and return a new value based on that state. This ensures that selectors are predictable and easy to reason about.


## Code Example:

Example of a todo list application

```javascript
import { atom } from 'recoil';

// Atom for storing list of todos
export const todoListState = atom({
  key: 'todoListState',
  default: [
    { id: 1, text: 'Example todo 1', completed: false },
    { id: 2, text: 'Example todo 2', completed: true },
    // Add more todo items here...
  ],
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
  - We define a selector __completedTodosCountSelector__ to compute the count of completed todos based on the current state of __todoListState__.
  - The __`get`__ function inside the selector retrieves the current value of __todoListState__ using __`get(todoListState)`__, filters the todos to get completed ones, and returns the count of completed todos.

## Usage:


```javascript
import { useRecoilValue } from 'recoil';
import { completedTodosCountSelector } from './selectors';

const CompletedTodosCount = () => {
  const completedCount = useRecoilValue(completedTodosCountSelector);

  return (
    <div>
      <p>Completed Todos Count: {completedCount}</p>
    </div>
  );
};

```
  - We use the __`useRecoilValue`__ hook to subscribe to the value of __completedTodosCountSelector__ and render the count of completed todos in the UI. Whenever the list of todos changes, Recoil automatically re-evaluates the selector and updates the UI accordingly.
