#  How `useQuery` and `useMutation` works?

Basically speaking __React Query__ helps with data fetching and mutation operations in React applications. It simplifies data fetching by handling loading, error, and success states automatically, and it provides caching and re-fetching capabilities too. 

React Query can be used in various types of data fetching : _RESTful APIs, GraphQL, Authentication and Authorization, Websockets and etc._


### Simplified way to think about it is that React Query has two main methods:

In a RESTful API context, these methods used for 
 - __`useQuery`__ : `GET` requests
 - __`useMutate`__ : `POST`, `PUT`, `DELETE` `PATCH` requests


Here is basic usgae to fetch data using `useQuery` :

   ```javascript
  import { useQuery } from 'react-query';
  
  const fetchTodos = async () => {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos');
    if (!response.ok) {
      throw new Error('Failed to fetch todos');
    }
    return response.json();
  };
  
  const TodosComponent = () => {
    const { data, isLoading, isError, error } = useQuery('todos', fetchTodos, {
      cacheTime: 300000, // Cache data for 5 minutes (300,000 milliseconds)
      staleTime: 60000, // Mark data as stale after 1 minute (60,000 milliseconds)
    });
  
    // Render UI...
  };
  
  
   ```
