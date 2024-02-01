#  How `useQuery` and `useMutation` works?

Basically speaking __React Query__ helps with data fetching and mutation operations in React applications. It simplifies data fetching by handling loading, error, and success states automatically, and it provides caching and re-fetching capabilities too. 

React Query can be used in various types of data fetching : _RESTful APIs, GraphQL, Authentication and Authorization, Websockets and etc._


### Simplified way to think about it is that React Query has two main methods:

In a RESTful API context, these methods used for 
 - __`useQuery`__ : `GET` requests
 - __`useMutate`__ : `POST`, `PUT`, `DELETE` `PATCH` requests
