# P2P Pong

A real-time, peer-to-peer multiplayer Pong game that runs entirely in your browser. Connect directly with a friend using a simple code—no servers required!

## How to Play

Pong is a classic two-player game where you control paddles to hit a ball back and forth. The first player to reach 10 points wins (you can change this in the code if desired).

### Objective
- Prevent the ball from reaching your side of the screen.
- Score points by getting the ball past your opponent's paddle.

### Controls
- **Mobile/Touch**: Touch and drag on the screen to move your paddle up and down.
- **Computer/Keyboard**: Use the Up/Down arrow keys or W/S keys to move your paddle.
- **Computer/Mouse**: Move your mouse over the game area to position your paddle.

## Getting Started

### Quick Start
1. Open `index.html` in a modern web browser (Chrome, Firefox, Safari, or Edge).
2. One player clicks "Host Game" to generate a unique code.
3. The other player enters that code and clicks "Join Game".
4. Start playing!

### Requirements
- A modern web browser with WebRTC support.
- **HTTPS connection** for P2P features (works on localhost for testing).
- For mobile play, deploy to a web server or use as a PWA.

### Testing Locally
- Open the file in two browser tabs/windows on the same computer.
- Host in one tab, join with the code in the other.

### Playing on Mobile
- Deploy `index.html` to a static web host (GitHub Pages, Netlify, etc.).
- Or run a local server: `python3 -m http.server` and access via your local IP.
- Add to home screen for a full-screen app experience.

## Features
- Real-time P2P multiplayer via WebRTC
- Responsive design that works on desktop and mobile
- Touch, keyboard, and mouse controls
- Automatic scaling to fit your screen
- No installation required—just open the HTML file

## Troubleshooting
- **Connection Issues**: Ensure both players are on HTTPS (or localhost).
- **Code Not Working**: Codes are case-sensitive and expire after use.
- **Mobile Not Working**: Try refreshing or redeploying to a server.
- **Audio Not Playing**: Some browsers require user interaction before audio (tap to start).

## Development
See `DEVELOPMENT.md` for technical details and future improvements.

Enjoy the game!</content>
<parameter name="filePath">c:\Users\aleks\projects\p2p-pong\README.md