## Handle authentication and generate JWT token:

It is a simplified example. In a real-world scenario, you would typically integrate this with a database for user management, use secure password hashing, and handle error cases more robustly. 

Additionally, you should always keep your secret key (`SECRET_KEY`) secure and never expose it in your codebase.

```javascript
// server.js

const express = require('express');
const jwt = require('jsonwebtoken');

const app = express();
const PORT = process.env.PORT || 3001;
const SECRET_KEY = 'your_secret_key'; //  a long, randomly generated string

app.use(express.json());

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

  // Generate JWT token
  const token = jwt.sign({ userId: user.id }, SECRET_KEY, { expiresIn: '1h' });

  res.json({ token });
});

app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});

```
In this server-side code:

 - We're using Express.js to create a simple HTTP server.
 - The `/api/login` endpoint handles user authentication. It expects a POST request with a JSON payload containing __`username`__ and __`password`__.
 - Upon receiving the credentials, it checks if they match any user in the mock database (__`users`__). If found, it generates a JWT token using the __`jsonwebtoken`__ library.
 - The generated token is then sent back to the client in the response.