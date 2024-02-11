## How Recoil differs from Redux: 

[Redux](https://redux.js.org/introduction/core-concepts) and [Recoil](https://recoiljs.org/docs/introduction/core-concepts) are most common state management tools used in UI frameworks. Although they are very similiar in what they do, the way they approach state management is completely different


While Redux's centralized store provides a single source of truth for application state, Recoil doesn't have a general store. Instead, Recoil manages state in a more decentralized manner using atoms and selectors.

### __In Recoil:__

- __Atoms__: Atoms are units of state that represent individual pieces of data in your application. Each atom manages a specific piece of state, such as user data, settings, or any other data your application needs to manage.

- __Selectors__: Selectors are used to derive state based on the current state of atoms. They allow you to compute derived values or perform transformations on state without directly modifying it.

Recoil provides hooks like `useRecoilState()` and `useRecoilValue()` to interact with atoms and selectors in your components. These hooks allow you to read and write state in a straightforward manner without the need for a centralized store.

### IMHO: Recoil's approach seems a lot easier to work with, __here is why:__ 

1. __Automatic updates and minimal boilerplate code.__ Recoil manages state updates by automatically re-evaluating selectors and components when atoms' values change. 

2. __More flexibility and simplicity__ for managing state in React applications. Each atom and selector manages its own piece of state, making it easy to reason about and maintain state in your application.






