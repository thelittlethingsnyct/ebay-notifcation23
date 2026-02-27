# ebay-notifcation23const express = require('express');
const crypto = require('crypto');
const app = express();

app.use(express.json());

const VERIFICATION_TOKEN = 'your_verification_token_here'; // you'll replace this
const ENDPOINT_URL = 'https://your-render-url.onrender.com/ebay-deletion'; // you'll replace this

app.get('/ebay-deletion', (req, res) => {
  const challengeCode = req.query.challenge_code;
  
  const hash = crypto.createHash('sha256')
    .update(challengeCode + VERIFICATION_TOKEN + ENDPOINT_URL)
    .digest('hex');

  res.json({ challengeResponse: hash });
});

app.post('/ebay-deletion', (req, res) => {
  console.log('eBay deletion notification received:', req.body);
  res.sendStatus(200);
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => console.log(`Server running on port ${PORT}`));
{
  "name": "ebay-deletion-endpoint",
  "version": "1.0.0",
  "main": "server.js",
  "scripts": {
    "start": "node server.js"
  },
  "dependencies": {
    "express": "^4.18.2"
  }
}
