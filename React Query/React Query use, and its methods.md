#  How React Query works with RESTful APIs?

 __React Query__ simplifies data fetching by __handling loading, error, and success states automatically__, and it provides caching and re-fetching capabilities too.

React Query can be used in various types of data fetching : _RESTful APIs, GraphQL, Authentication and Authorization, Websockets and etc._


## You just need to know two methods `useQuery` and `useMutation`: 

In a RESTful API context, these methods used for 
 - __`useQuery`__ : `GET` requests
 - __`useMutate`__ : `POST`, `PUT`, `DELETE` `PATCH` requests


Here is basic usage to fetch data using `useQuery` :

   ```javascript
  import { useQuery } from 'react-query';
  
  const fetchUsers = async () => {
    const response = await fetch('https://someApiAddress/users');
    if (!response.ok) {
      throw new Error('Failed to fetch users');
    }
    return response.json();
  };
  
  const UsersComponent = () => {
    const { data, isLoading, isError, error, refetch } = useQuery('users', fetchUsers, {
      cacheTime: 300000, // Cache data for 5 minutes (300,000 milliseconds)
      staleTime: 60000, // Mark data as stale after 1 minute (60,000 milliseconds)
    });
  

   const handleRefresh = () => {
    refetch(); // Manually trigger a refetch
   };

    return (
      <div>
        <h1>Users</h1>

        <button onClick={handleRefresh}>Refresh</button>

        {isLoading && <div>Loading...</div>}

        {isError && <div>Error: {error.message}</div>}

        {data && (
          <ul>
            {data.map(user => (
              <li key={user.id}>{user.name}</li>
            ))}
          </ul>
        )}
      </div>
    );
   };
   ```

As you can see it provides with `isLoading`, `isError`, `error` states and `data` which you can directly use in your UI

-  __`refetch`__ (optional):  fetches fresh data from the API and updates the query's cache.
  
- __` useQuery('users', .. `__ 'users' in here is a Query key, you need to come up with unique key for the data ur fetching, so that React Query can label it for future mutations or caching.
  
- __`cacheTime`__ (optional): You can specify how long query data should remain in the cache.

- __`staleTime`__ (optional): You can define a time threshold after which query data becomes stale and requires refetching.

  _In real case you most likely use only one of the: `refetch` or  `cacheTime` or `cacheStale` to refetch data, not all of them together as in this example._


## How `useMutate` works:
  Unless you want to edit chached data too, you don't need a Query Key with __`useMutate`__. 

  Here's simple use case: 

   ```javascript
        const createNewUser = async (newUser) => {
          const response = await fetch('https://someApiAdress/users', {
            method: 'POST',
            headers: {
              'Content-Type': 'application/json',
            },
            body: JSON.stringify(newUser),
          });
          if (!response.ok) {
            throw new Error('Failed to create new user');
          }
          return response.json();
        };
        
        const UserForm = () => {
          const [newUser, setNewUser] = useState('');
          const { mutate, isLoading, isError, error } = useMutate(createNewUser);
        
          const handleSubmit = async (event) => {
            event.preventDefault();
            try {
              await mutate(newUser); // Call the mutate function with the new user
              setNewUser(''); // Clear the input field after successful mutation
            } catch (error) {
              console.error('Error creating todo:', error);
            }
          };
        
          return (
            <form onSubmit={handleSubmit}>
              <input
                type="text"
                value={newUser}
                onChange={(event) => setNewUser(event.target.value)}
                placeholder="Enter Your Name"
              />
              <button type="submit" disabled={isLoading}>Add User</button>
              {isError && <div>Error: {error.message}</div>}
            </form>
          );
        };
        
   
  ```

  
  - When the user submits the form, we call the `mutate` function with the new name data to create the new user.
  - We handle loading, error, and success states using `isLoading`, `isError`, and `error`.

### `useMutate` has two optional parameters: `retry` and `onMutate`: 

ps: Here you need to provide Query Key of the data collection you want to edit

```javascript

   const { mutate, isLoading, isError, error } = useMutate(createNewUser, {
     retry: 3, // Retry the mutation up to 3 times before giving up
     onMutate: async (newUser) => {
       const currentTodos = queryClient.getQueryData('users');  // Query KEY
       // Update UI optimistically
       queryClient.setQueryData('users', (old) => [...old, { id: Date.now(), title: newUser }]);
       return { currentUsers }; // Save current state for rollback
     },
     onError: (error, variables, rollback) => {
       // Rollback the optimistic update if the mutation fails
       rollback(); // Revert UI to its previous state
     },
   });
   
   const handleSubmit = async (event) => {
     event.preventDefault();
     try {
       await mutate(newTodo);
       setNewTodo('');
     } catch (error) {
       console.error('Error creating todo:', error);
     }
   };
   
   // Inside the onError callback, you would implement the logic to revert the optimistic update
   
   onError: (error, variables, rollback) => {
     // Revert UI to its previous state by rolling back the optimistic update
     const { currentUsers } = variables;
     queryClient.setQueryData('users', currentUsers); // Restore previous state
   },
   


```
- We use the __`retry`__ option to specify that the mutation should be retried up to 3 times before giving up.

- We use the __`onMutate`__ option to define an __optimistic update__. Before the mutation occurs, we save the current state of todos and update the UI optimistically with the new todo.

  -  __Optimistic Update__: Before sending the mutation request to the server, you update the UI as if the mutation has already succeeded, even though the server response is pending.

  -  __Rollback__ (if needed): In case of a failed mutation, you might need to roll back the optimistic update to bring the UI back to its original state before the user action.
  
- __`queryClient`__, comes from React Query setup at the root level of your React component tree, such as in your index.js or App.js file.

This is how you usually set up React Query for your react app: 

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import { QueryClient, QueryClientProvider } from 'react-query';
import { ReactQueryDevtools } from 'react-query/devtools';

import App from './App';

const queryClient = new QueryClient();

ReactDOM.render(
  <React.StrictMode>
    <QueryClientProvider client={queryClient}>
      <App />
      <ReactQueryDevtools initialIsOpen={false} /> {/* Optional: Devtools for debugging */}
    </QueryClientProvider>
  </React.StrictMode>,
  document.getElementById('root')
);


```
