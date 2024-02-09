## React Query Auth:
React Query Auth is a library that integrates seamlessly with React Query to simplify authentication and authorization in React applications. 

It works smoothly with React Query, giving easy hooks to handle user stuff without any fuss. It's the simple solution for hassle-free authentication! 

### Key Hooks:

- __`useAuth`__: Handles login, signup, logout, user data, and authentication state.
  
  - `login(credentials)`: Tries to log in the user with the provided credentials.
  - `signup(data)`: Registers a new user with the given data.
  - `logout()`: Logs out the user and clears authentication state.
  - `user`: Gives access to the current logged-in user information (read-only).
  - `status`: Shows the current authentication state (read-only).
    
- __`isAuthenticated`__: Tells if a user is currently logged in (calculated property).
  
- __`useIsAuthorized`__: Checks if the current user is allowed to access specific protected routes or data.
  
- __`useLogoutMutation`__: Provides a mutation function specifically for logging out the user.

- __`useRefreshMutation`__: (Optional) Offers a mutation function for refreshing access tokens if needed.
