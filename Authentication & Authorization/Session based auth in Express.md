## Session-Based Authentication:

 - Session-based authentication involves the use of server-side sessions to manage user authentication.
 - When a user logs in, the server creates a session for the user and stores session data on the server.
 - The server sends a session ID to the client, typically in the form of a cookie.
 - The client includes the session ID in subsequent requests, and the server uses it to look up the corresponding session data and authenticate the user.
 - Sessions are typically stored in memory or a distributed cache like Redis on the server side.

   ```javascript
      const express = require('express');
      const session = require('express-session');
      const bodyParser = require('body-parser');
      
      const app = express();
      const PORT = process.env.PORT || 3001;
      const SECRET_KEY = 'your_secret_key';
      
      // Middleware
      app.use(bodyParser.json());
      app.use(session({
        secret: SECRET_KEY,
        resave: false,
        saveUninitialized: true,
        cookie: { secure: false } // Set to true in production for HTTPS
      }));
      
      // Mock user database
      const users = [
        { id: 1, username: 'user1', password: 'password1' },
        { id: 2, username: 'user2', password: 'password2' }
      ];
      
      // Login endpoint
      app.post('/api/login', (req, res) => {
        const { username, password } = req.body;
      
        // Find user by username and password
        const user = users.find(u => u.username === username && u.password === password);
      
        if (!user) {
          return res.status(401).json({ error: 'Invalid username or password' });
        }
      
        // Store user ID in session
        req.session.userId = user.id;
      
        res.json({ message: 'Login successful' });
      });
      
      // Restricted endpoint
      app.get('/api/restricted', (req, res) => {
        // Check if user is authenticated (user ID is stored in session)
        if (!req.session.userId) {
          return res.status(401).json({ error: 'Unauthorized' });
        }
      
        // Authenticate user based on user ID stored in session
        const authenticatedUser = users.find(u => u.id === req.session.userId);
      
        if (!authenticatedUser) {
          return res.status(401).json({ error: 'Unauthorized' });
        }
      
        // Access granted
        res.json({ message: 'Access granted to restricted endpoint' });
      });
      
      // Logout endpoint
      app.post('/api/logout', (req, res) => {
        // Destroy session to log out user
        req.session.destroy(err => {
          if (err) {
            console.error('Error destroying session:', err);
            return res.status(500).json({ error: 'Logout failed' });
          }
          res.json({ message: 'Logout successful' });
        });
      });
      
      app.listen(PORT, () => {
        console.log(`Server is running on port ${PORT}`);
      });


   ```
