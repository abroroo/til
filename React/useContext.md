I found mysef googling a lot the same stuff like how to use `useContext` React hook.

So I decided to put it here. It is a simple code snippet that I can come back to whenever I need to brush up on this.

## How useContext works:
Pass data through the component tree without having to pass props manually at every level. 
It allows to share values like authentication state, theme, or localization preferences across components without explicitly passing them through props.

1. __Create Context:__

   First, you create a context object using React.createContext().

3. __Provide Context:__

    Then, you wrap the part of your component tree where you want to provide the context with a Context.Provider component. You pass the value you want to share as a prop to the Provider.

3. __Consume Context:__

    Inside a functional component, you use the useContext hook to access the value of the context. You pass the context object (created in step 1) as an argument to useContext, and it returns the current context value.


```javascript
import React, { createContext, useContext } from 'react';

// Step 1: Create Context
const MyContext = createContext();

// Step 2: Provide Context
const App = () => {
  return (
    <MyContext.Provider value="Hello from Context">
      <ChildComponent />
    </MyContext.Provider>
  );
};

// Step 3: Consume Context
const ChildComponent = () => {
  const contextValue = useContext(MyContext);

  return <div>{contextValue}</div>;
};

export default App;


```
