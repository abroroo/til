## Session-Based Authentication:

 - Session-based authentication involves the use of server-side sessions to manage user authentication.
 - When a user logs in, the server creates a session for the user and stores session data on the server.
 - In session-based authentication, the session ID can be transmitted to the client in various ways, including __cookies__, __URL parameters__, or __custom headers__.
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
In this example:

 - We're using the __`express-session`__ middleware to manage sessions in Express.js. Sessions are stored in memory by default, but you can configure other session stores like Redis for production use.
 - When a user logs in (__`/api/login`__), we store the user's ID in the session (__`req.session.userId`__).
 - For a restricted endpoint (__`/api/restricted`__), we check if the user is authenticated by verifying that their user ID is stored in the session. If authenticated, access is granted.
 - We also provide a logout endpoint (__`/api/logout`__) to destroy the session and log out the user.
