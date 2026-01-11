# P2P Pong - Developer Guide

## 1. Overview
P2P Pong is a serverless, real-time multiplayer game that runs entirely in the browser. It allows two players to connect directly via WebRTC using a unique 6-character code. The entire application (HTML, CSS, Game Logic, Networking) is contained within a single `index.html` file, making it extremely portable and easy to deploy.

## 2. Architecture

### Core Technology
* **HTML5 Canvas:** Handles high-performance 2D rendering (60 FPS).
* **PeerJS (WebRTC):** Manages the handshake and establishes a direct Peer-to-Peer data channel between devices.
* **Data URI Manifest:** Enables "Add to Home Screen" functionality on Android without external JSON files.

### Network Topology
The game uses a **Host-Authoritative** model:
1.  **Player 1 (Host):** Runs the game physics (ball movement, collision detection, scoring). They send the "Game State" (ball position, score) to Player 2.
2.  **Player 2 (Client):** Sends only their input (Paddle Y position) to the Host. They receive the "Game State" and render it blindly.

This ensures the game state remains synchronized, as only one device (the Host) decides where the ball actually is.

## 3. Getting Started

### Prerequisites
* A modern web browser (Chrome, Firefox, Safari).
* **HTTPS:** WebRTC requires a secure context. You cannot test P2P features on mobile using `file://`.
* *Local Testing:* You can test on `localhost` (which browsers treat as secure).

### Running Locally
1.  Download `index.html`.
2.  Open the file directly in a browser on your computer.
3.  **To test P2P:** Open the file in two separate browser tabs/windows.
    * Tab 1: Click "Host Game". Copy the code.
    * Tab 2: Paste the code and click "Join Game".

### Deployment
To play on mobile devices, deploy the file to a static host:
* **GitHub Pages:** Push to a repo and enable Pages.
* **Netlify/Vercel:** Drag and drop the `index.html` file.
* **Python Server (Local WiFi):** Run `python3 -m http.server` and access via your computer's local IP (Note: some browsers block WebRTC on HTTP local IP).

## 4. Code Structure
The `index.html` file is divided into three logical sections:

1.  **CSS (`<style>`):** Handles the "Cyberpunk/Retro" aesthetic, UI layering, and responsive canvas scaling.
2.  **HTML (`<body>`):** Contains the UI overlays (Main Menu, Waiting Screen) and the `<canvas>` element.
3.  **JavaScript (`<script>`):**
    * **Config:** Constants for ball speed, paddle size, etc.
    * **Networking:** PeerJS initialization and data handling (`handleData`).
    * **Game Loop:** The `update()` and `draw()` functions running on `requestAnimationFrame`.
    * **Input:** Touch event listeners mapped to paddle coordinates.

## 5. Key Functions

| Function | Role |
| :--- | :--- |
| `initPeer()` | Connects to the public PeerJS signaling server to get an ID. |
| `hostGame()` | Sets `isHost = true`, initializes peer, and waits for connection. |
| `joinGame()` | Sets `isHost = false`, connects to the Host ID. |
| `update()` | **Host Only.** Calculates physics, collisions, and sends state to Client. |
| `handleData(data)` | Routes incoming packets. Host listens for `move`; Client listens for `state`. |

## 6. Future Improvements / Roadmap

If you wish to expand this project, here are the recommended next steps:


### 0. Create PWA Manifest file
* Make the page look & feel like a native mobile application.

### 1. Lag Compensation (Interpolation)
* **Current Issue:** If the network hiccups, the ball might teleport on the Client's screen.
* **Fix:** Instead of snapping the ball to the received X/Y immediately, the Client should smooth the movement between the current position and the new target position (Linear Interpolation or Lerp).

### 2. Audio Support
* Add simple `AudioContext` beeps for paddle hits and scoring.
* *Note:* Browsers require user interaction (a tap) before playing audio, so initialize audio on the "Host/Join" button click.

### 3. Reconnection Logic
* Currently, if a player minimizes the browser, the connection might close.
* Add logic to handle `conn.on('close')` gracefully, perhaps pausing the game and waiting for a reconnect.

### 4. Code Refactoring
* As the logic grows, split the single file into `game.js`, `network.js`, and `style.css` for better maintainability during development (you can use a bundler like Parcel/Vite to merge them back into one file for deployment).

### 5. Enhanced Mobile UX
* Add "Safe Areas" for iPhone notches.
* Implement a "Full Screen" button API trigger for browsers that support it.
