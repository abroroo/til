## Session-Based Authentication:

 - Session-based authentication involves the use of server-side sessions to manage user authentication.
 - When a user logs in, the server creates a session for the user and stores session data on the server.
 - In session-based authentication, the session ID can be transmitted to the client in various ways, including __cookies__, __URL parameters__, or __custom headers__.
 - The client includes the session ID in subsequent requests, and the server uses it to look up the corresponding session data and authenticate the user.
 - Sessions are typically stored in memory or a distributed cache like Redis on the server side.
