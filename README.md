# Project IOT Smart chair

An IoT project that uses pressure sensors on a chair and computer vision (PoseNet) to analyze and improve sitting posture.
## Features

- Real-time posture monitoring using pressure sensors (FSR)
- Computer vision posture analysis using PoseNet
- Web interface with real-time feedback
- MongoDB database for data storage
- Elegant UI design with EB Garamond font


## System Architecture

1. **ESP32 with FSR sensors** - Collects pressure data from the chair
2. **Node.js Express Server** - Processes data from ESP32 and PoseNet
3. **PoseNet** - Computer vision for posture detection
4. **MongoDB** - Stores historical posture data
5. **Web Interface** - Provides feedback

## Prerequisites

- Node.js (v14 or higher)
- MongoDB (or Docker for containerized setup)
- ESP32 with FSR sensors configured
- Webcam for PoseNet functionality

## Installation

### 1. Installa le dipendenze del Server
Naviga nella directory server ed esegui:
```bash
cd server
npm install
```

### 2. Install Client Test Dependencies (if needed)
Navigate to the clients/Tests directory and run:
```bash
cd clients/Tests
npm install
```
### 3. Start Services (e.g., Database via Docker)
If you use docker-compose.yml to manage services like a database, from the server directory run:
```bash
docker-compose up -d
```
### 4. Start the Server
From the project root or the server directory, start the server (the command may vary depending on how package.json or start.js is configured):
```bash
cd server
npm start
```

## Configure the Arduino
The code for the Arduino client is located in clients/arduino/arduinoClient/.

1. Go to the smartchair/clients/arduino/arduinoClient directory.
2. Open the file config.h.
3. Replace the default values with your own:
```
const char* ssidHotspot = "Your Wi-Fi name";
const char* passwordHotspot = "Password";
String serverIP = "Your local IP";
String chairName = "Your chair name";
```
Replace "Your Wi-Fi name", "Password", and "Your local IP" with
your actual network’s SSID, password, and the server’s IP address.
Replace "Your chair name" with a unique string that identifies your
chair. This allows the server and client to distinguish your device from
others on the network.
4. Upload the arduinoClient.ino sketch to your Arduino/ESP32 device.
4. Make sure the sensors are connected correctly.
## System Usage
1. Make sure the Arduino client  is powered and connected to the WiFi network, and is sending data to the server.
2. Start the Node.js server.
3. Open the web interface (chairFrontend/index.html) in your browser.
4. If Posenet is integrated and active, grant webcam permissions when requested.
5. The system should start analyzing posture.
## Project Structure
```
smartchair/
├── README.md                   # This file
├── clients/                    # Client code
│   ├── Tests/                  # Client tests
│   │   ├── chair.test.js
│   │   ├── main.test.js
│   │   ├── package-lock.json
│   │   ├── package.json
│   │   └── posenet.test.js
│   ├── arduino/                # Arduino client code
│   │   └── arduinoClient/      # Arduino client sources (e.g., .ino files)
│   │       ├── config.h
│   │       └── arduinoClient.ino
│   └── chairFrontend/          # Web user interface
│       ├── .idea/
│       ├── css/
│       ├── index.html
│       └── js/
└── server/                     # Server application code
    ├── Tests/
    │   └── server.test.js
    ├── docker-compose.yml
    ├── package-lock.json
    ├── package.json
    ├── server/
    │   └── server.js
    └── start.js

```