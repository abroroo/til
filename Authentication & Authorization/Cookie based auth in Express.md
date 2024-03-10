## Cookie-based Authentication:

 - __Cookie-based authentication__ is a specific implementation of session-based authentication where the session ID is stored in a cookie on the client side.
 - When a user logs in, the server creates a session and sets a cookie containing the session ID in the HTTP response.
 - The browser automatically includes the cookie in subsequent requests to the same domain.
 - The server reads the session ID from the cookie and uses it to retrieve the user's session data and authenticate them.
 - Cookies can have additional attributes like expiration time, domain, and secure flag to control their behavior.
   
   Sample implementation in Express.js
  ```javascript
    const express = require('express');
    const cookieParser = require('cookie-parser');
    
    const app = express();
    const PORT = process.env.PORT || 3001;
    const SECRET_KEY = 'your_secret_key';
    
    app.use(express.json());
    app.use(cookieParser());
    
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
    
      // Generate session ID (you can use a library like `uuid`)
      const sessionId = generateSessionId();
    
      // Set session ID as a cookie
      res.cookie('sessionId', sessionId, { httpOnly: true });
    
      res.json({ message: 'Login successful' });
    });
    
    // Restricted endpoint
    app.get('/api/restricted', (req, res) => {
      // Check if session ID is present in the cookie
      const sessionId = req.cookies.sessionId;
    
      if (!sessionId) {
        return res.status(401).json({ error: 'Unauthorized' });
      }
    
      // Authenticate user based on session ID
      // (You would typically validate the session ID against a session store)
      // For simplicity, we'll just check if the session ID is valid
      if (isValidSessionId(sessionId)) {
        return res.json({ message: 'Access granted to restricted endpoint' });
      } else {
        return res.status(401).json({ error: 'Unauthorized' });
      }
    });
    
    app.listen(PORT, () => {
      console.log(`Server is running on port ${PORT}`);
    });


   ```
