
## JWT vs Session
The main difference lies in where the authentication information is stored:
 - With __JWT authentication__, the authentication information is stored in the token itself, which is typically stored on the client side (e.g., in memory or local storage).
 - With __session-based authentication__, the session ID is stored in the cookie on the client side, while the authentication information (e.g., user ID, authentication status) is stored on the server side, often in a session store like Redis.

## Cookie based vs Session based
__Cookies-Based Authentication:__ 
 - Authentication data is stored in a cookie on the user's browser, including login credentials.
 - The server sends this cookie with every subsequent request made by the user to maintain their authenticated state.
   
__Session-Based Authentication:__
 - Authentication data is saved on the server side, typically in the form of a session object.
 - A session ID, which is generated and linked to a user's account upon login, is stored on the user's browser as a cookie.
 - The session ID is sent to the server with each subsequent request, allowing the server to look up the user's authentication details and maintain their authenticated state.


 
