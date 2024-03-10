## Session-Based Authentication:

 - Session-based authentication involves the use of server-side sessions to manage user authentication.
 - When a user logs in, the server creates a session for the user and stores session data on the server.
 - In session-based authentication, the session ID can be transmitted to the client in various ways, including __cookies__, __URL parameters__, or __custom headers__.
 - The client includes the session ID in subsequent requests, and the server uses it to look up the corresponding session data and authenticate the user.
 - Sessions are typically stored in memory or a distributed cache like Redis on the server side.

Example using URL parameters: 

```javascript
const express = require('express');
const bodyParser = require('body-parser');

const app = express();
const PORT = process.env.PORT || 3001;
const SECRET_KEY = 'your_secret_key';

// Middleware
app.use(bodyParser.json());

// Mock user database
const users = [
  { id: 1, username: 'user1', password: 'password1' },
  { id: 2, username: 'user2', password: 'password2' }
];

// Session store
const sessions = {};

// Login endpoint
app.post('/api/login', (req, res) => {
  const { username, password } = req.body;

  // Find user by username and password
  const user = users.find(u => u.username === username && u.password === password);

  if (!user) {
    return res.status(401).json({ error: 'Invalid username or password' });
  }

  // Create session ID
  const sessionId = generateSessionId();
  
  // Store session ID in session store
  sessions[sessionId] = user.id;

  res.json({ message: 'Login successful', sessionId });
});

// Restricted endpoint
app.get('/api/restricted/:sessionId', (req, res) => {
  const sessionId = req.params.sessionId;

  // Check if session ID is valid and user is authenticated
  if (!sessions[sessionId]) {
    return res.status(401).json({ error: 'Unauthorized' });
  }

  // Authenticate user based on session ID
  const userId = sessions[sessionId];
  const authenticatedUser = users.find(u => u.id === userId);

  if (!authenticatedUser) {
    return res.status(401).json({ error: 'Unauthorized' });
  }

  // Access granted
  res.json({ message: 'Access granted to restricted endpoint' });
});

// Logout endpoint
app.post('/api/logout/:sessionId', (req, res) => {
  const sessionId = req.params.sessionId;

  // Remove session from session store
  delete sessions[sessionId];

  res.json({ message: 'Logout successful' });
});

app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});

// Function to generate a random session ID
function generateSessionId() {
  return Math.random().toString(36).substring(2, 15) + Math.random().toString(36).substring(2, 15);
}


```
 - The session ID is included as a URL parameter in the endpoints (__`/api/restricted/:sessionId`__ and __`/api/logout/:sessionId`__).
 - When logging in, the server generates a session ID and sends it back to the client in the response.
 - For subsequent requests, the client includes the session ID as a URL parameter.
 - The server validates the session ID from the URL parameter to authenticate the user.
