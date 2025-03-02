# Roblox Script Hub Admin Dashboard

A WebSocket-based admin dashboard for managing Roblox script users. This dashboard allows you to monitor connected clients and send commands to them remotely.

## Features

- Real-time monitoring of connected Roblox clients
- Send commands to individual clients or all clients at once
- Password-protected admin interface
- Support for commands like messaging and kicking players

## Setup

1. Install dependencies:
   ```
   npm install
   ```

2. Configure environment variables:
   - Copy `.env.example` to `.env` (or use the existing `.env` file)
   - Update the `ADMIN_PASSWORD` in the `.env` file

3. Start the server:
   ```
   npm start
   ```

4. Access the admin dashboard:
   - Open `http://localhost:3000` in your browser
   - Login with the password set in the `.env` file

## Client Integration

The Roblox client script should connect to the WebSocket server at `ws://your-server-address:3000` and send a registration message with the following format:

```lua
local registrationMessage = HttpService:JSONEncode({
    action = "register",
    jobId = jobId,
    userId = userId,
    username = username,
    gameName = gameName,
})
WS:Send(registrationMessage)
```

## Available Commands

- **Message**: Send a text message to the client
- **Kick**: Kick the player with an optional reason

## Deployment

For production deployment:

1. Set a strong `ADMIN_PASSWORD` and `SESSION_SECRET` in the `.env` file
2. Consider using a process manager like PM2:
   ```
   npm install -g pm2
   pm2 start server.js
   ```
3. Set up a reverse proxy (like Nginx) to handle HTTPS

## Security Considerations

- Change the default admin password in the `.env` file
- In production, set up HTTPS using a reverse proxy
- Consider implementing rate limiting for login attempts