# JWT Workflow:

1. __Login__: The user submits credentials (username/password) to the server.
2. __Authentication__: The server validates the credentials and retrieves user information.
3. __Token Generation__: The server creates a JWT payload with user claims and signs it with a secret key.
4. __Token Response__: The server sends the JWT back to the client (usually stored in local storage or cookies).
5. __Secured Requests__: On subsequent requests, the client includes the JWT in the Authorization header using the "Bearer" scheme (e.g., "Authorization: Bearer <token>").
6. __Token Validation__: The server receives the JWT, extracts the header and payload, and verifies the signature using its secret key.
7. __Authorization__: If the token is valid, the server grants access to the requested resource based on the user information in the claims.


# Session Workflow

1. __Login__:  The user enters their credentials (username and password) on the login page.
2. __Authentication__: The server receives the credentials and verifies them against a user database (often using hashing algorithms for password security).
3. __Session Creation__: If valid, the server creates a session on its side. This session can be stored in memory, database, or a file system. The session typically contains:
   - Session ID: A unique identifier for the session.
   - User Data: Essential user information like user ID, username, roles, etc.
   - Creation Time: Timestamp of session creation.
   - Expiration Time: Timeout period for the session (inactivity triggers session termination).
4. __Session ID Transfer__:  The server generates a session ID (often a random string) and transmits it to the client (user's browser)  typically  through a:
5. __Cookie__: A small piece of data stored on the user's device by the browser. It holds the session ID and is included in subsequent requests to the server.
6. __Subsequent Requests and Verification__:

   - Secured Requests: With each subsequent request to the application, the user's browser automatically sends the cookie containing the session ID back to the server.
   - Session ID Lookup: The server receives the request and retrieves the session data associated with the provided session ID from its storage (memory, database, etc.).
   - Authorization: If a valid session is found (not expired or invalidated), the server grants access to the requested resource based on the user information stored in the session data.
   - Session Renewal (Optional): Some implementations might refresh the session expiration time on user activity to extend the session duration.
