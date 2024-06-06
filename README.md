# Real-time Chat Application
Develop a chat app using WebSocket technology to enable real-time
communication.
  # Create a new directory for your project
    mkdir chat-app

# Navigate into the project directory
    cd chat-app

# Initialize a new Node.js project with default settings
    npm init -y

# Install the required dependencies
    npm install ws express

    const express = require('express');
    const WebSocket = require('ws');

    const app = express();
    const port = 3000;

    // Serve static files from the public directory
    app.use(express.static('public'));

    const server = app.listen(port, () => {
      console.log(`Server is listening on http://localhost:${port}`);
    });

    const wss = new WebSocket.Server({ server });

    wss.on('connection', (ws) => {
      console.log('New client connected');

      ws.on('message', (message) => {
        console.log(`Received: ${message}`);
        // Broadcast the message to all clients
        wss.clients.forEach((client) => {
          if (client !== ws && client.readyState === WebSocket.OPEN) {
            client.send(message);
          }
        });
      });

      ws.on('close', () => {
        console.log('Client disconnected');
       });
    });
    <!DOCTYPE html>
    <html lang="en">
    <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Real-time Chat App</title>
    <style>
        body { font-family: Arial, sans-serif; }
        #chat { margin-bottom: 20px; }
        #messages { border: 1px solid #ccc; height: 300px; overflow-y: scroll; padding: 10px; }
        #input { width: calc(100% - 22px); }
    </style>
    </head>
    <body>
    <div id="chat">
        <div id="messages"></div>
        <input type="text" id="input" placeholder="Type a message..." autofocus>
    </div>
    <script>
        const ws = new WebSocket(`ws://${location.host}`);

        ws.onmessage = (event) => {
            const messages = document.getElementById('messages');
            const message = document.createElement('div');
            message.textContent = event.data;
            messages.appendChild(message);
            messages.scrollTop = messages.scrollHeight;
        };

        document.getElementById('input').addEventListener('keypress', (event) => {
            if (event.key === 'Enter') {
                const input = document.getElementById('input');
                const message = input.value;
                ws.send(message);
                input.value = '';
            }
        });
    </script>
    </body>
    </html>
    node server.js
