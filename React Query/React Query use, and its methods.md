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

  That's the basics of using __useMutate__! It simplifies data mutation in React applications and provides a convenient way to manage loading, error, and success states during mutation operations.
