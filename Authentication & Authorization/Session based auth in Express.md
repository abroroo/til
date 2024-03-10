> I'm saving this sample snippet for myself, so that I can refer to it whenever I need quick look up.

## Session-Based Authentication:
 - Authentication data is saved on the server side, typically in the form of a session object.
 - A session ID, which is generated and linked to a user's account upon login, is stored on the user's browser as a cookie.
 - The session ID is sent to the server with each subsequent request, allowing the server to look up the user's authentication details and maintain their authenticated state.

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
