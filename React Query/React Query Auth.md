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


### How to use it: 

__1. Authentication with `useAuth` hook__:

  ```javascript
  function Login() {
    const { login, status } = useAuth();
  
    const handleSubmit = async (event) => {
      event.preventDefault();
      const username = event.target.username.value;
      const password = event.target.password.value;
      await login({ username, password });
    };
  
    return (
      <form onSubmit={handleSubmit}>
        {/* Login form  */}
        <button type="submit">Login</button>
        {status === 'loading' && <p>Logging in...</p>}
        {status === 'error' && <p>Login failed!</p>}
      </form>
    );
  }
  
  
  ```

__2. Authorization with `useIsAuthorized` hook:__

  ```javascript
  function ProtectedContent() {
    const isAuthorized = useIsAuthorized();
  
    if (!isAuthorized) return <p>Unauthorized</p>;
  
    // Fetch and display protected data
    const { data } = useQuery('protectedData', fetchData);
  
    return (
      <div>
        {/* Something private */}
      </div>
    );
  }
  
  
  ```

__3. Data fetching with `useQuery` of React Query for Authentication:__

  ```javascript
  const { data, isLoading, error } = useQuery('userData', fetchUserData);
  
  if (isLoading) return <p>Loading...</p>;
  if (error) return <p>Error: {error.message}</p>;
  
  return (
    <div>
      {/* User Profile maybe  */}
    </div>
  );
  
  
  ```

__4. Logout with `useLogout` hook:__

  ```javascript
  function LogoutButton() {
    const logout = useLogout();
  
    const handleClick = () => {
      logout();
    };
  
    return <button onClick={handleClick}>Logout</button>;
  }
  
  ```

With this you can reduce boilerplate code by handling authentication state
