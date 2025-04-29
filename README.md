ESP8266 Smart Controller 🌐💡

![image](https://github.com/user-attachments/assets/77ef9d48-0005-4a4e-a834-a3ce389f0885)




✨ Features

Modern Web Interface: Sleek, card-based UI with responsive design
Multi-pin Control: Control GPIO pins 4, 5, and the built-in LED
Real-time Status: Visual indicators show the current state of each pin
Auto-Blink Mode: Special mode for automatic LED blinking without blocking the main process
Live Clock: JavaScript-powered real-time clock display
Mobile Friendly: Works seamlessly on smartphones and tablets
Connection Status: Displays device IP and connection information

📋 Requirements
Hardware

ESP8266-based board (NodeMCU, Wemos D1 Mini, etc.)
LED(s) or other components connected to GPIO pins 4 and 5 (optional)
Micro USB cable

Software

Arduino IDE
ESP8266 Board Package
ESP8266WiFi Library

🛠️ Installation

Set up Arduino IDE

Install the Arduino IDE
Add ESP8266 support via Boards Manager
Install required libraries (ESP8266WiFi comes with the ESP8266 board package)


Clone the Repository
bashgit clone https://github.com/yourusername/esp8266-smart-controller.git
cd esp8266-smart-controller

Configure the Code

Open esp8266_smart_controller.ino in the Arduino IDE
Update the WiFi credentials with your network details:
cppconst char* ssid     = "YOUR_WIFI_SSID";
const char* password = "YOUR_WIFI_PASSWORD";



Upload to Your ESP8266

Connect your ESP8266 board via USB
Select the correct board and port in the Arduino IDE
Click the Upload button


Access the Control Panel

Open the Serial Monitor (9600 baud) to see the assigned IP address
Enter this IP address in your web browser
The control interface should appear



📊 How It Works
The ESP8266 Smart Controller creates a web server on your local network. When accessed via a web browser, it serves an interactive HTML interface that allows you to:

Control the state of GPIO pins 4 and 5 (ON/OFF)
Control the built-in LED (ON/OFF/BLINK)
View real-time status information

The system uses non-blocking techniques to handle multiple tasks simultaneously:

Web server processing
LED blinking (when enabled)
Status monitoring

🔧 Customization
Changing GPIO Pins
To change which pins are controllable, modify these constants:
cppconst int output5 = 5;  // Change to your desired pin
const int output4 = 4;  // Change to your desired pin
// LED_BUILTIN is automatically defined
Customizing the UI
The web interface is defined in the loop() function. You can modify the HTML, CSS, and JavaScript to customize:

Colors and styling
Layout and organization
Button behavior
Add additional controls

Adding More Pins
To add more controllable pins:

Define new pin variables and states
Initialize them in the setup() function
Add handling in the HTTP request processing section
Add the corresponding UI elements in the HTML section

🧩 Project Structure
esp8266-smart-controller/
├── esp8266_smart_controller.ino  # Main Arduino sketch
├── README.md                     # This documentation
├── LICENSE                       # MIT License file
└── assets/                       # Images and resources
    └── project-preview.png       # UI preview image
🌐 Network Configuration

Web Server Port: 80 (standard HTTP)
IP Address: Dynamically assigned via DHCP
Timeout: 2000ms (connection timeout for clients)

⚡ Advanced Features
Non-blocking LED Blink
The code uses the millis() function for timing instead of delay(), allowing the LED to blink without blocking other operations:
cppif (autoBlinkEnabled) {
  unsigned long currentMillis = millis();
  if (currentMillis - previousBlinkMillis >= blinkInterval) {
    previousBlinkMillis = currentMillis;
    // Toggle the LED state
    if (digitalRead(LED_BUILTIN) == LOW) {
      digitalWrite(LED_BUILTIN, HIGH);
      builtInLedState = "on";
    } else {
      digitalWrite(LED_BUILTIN, LOW);
      builtInLedState = "off";
    }
  }
}
Real-time JavaScript Clock
The web interface includes a JavaScript clock that updates in real-time:
javascriptfunction updateClock() {
  const now = new Date();
  const timeElem = document.getElementById('current-time');
  timeElem.textContent = now.toLocaleTimeString();
}

window.onload = function() {
  setInterval(updateClock, 1000);
  setInterval(updateStatus, 1000);
};
🔄 Future Enhancements

 Add MQTT support for IoT integration
 Implement OTA (Over-The-Air) updates
 Add user authentication
 Create scheduling functionality
 Implement sensor data visualization
 Add HTTPS support
 Create mobile app companion

🐛 Troubleshooting
Cannot Connect to WiFi

Verify your SSID and password are correct
Ensure your router is functioning properly
Check if your ESP8266 is within WiFi range

Web Interface Not Loading

Verify the IP address in your browser
Check if your device is connected to the same network
Try restarting the ESP8266

Pins Not Responding

Check your wiring connections
Verify the pin numbers in the code
Ensure your ESP8266 board is properly powered

📜 License
This project is licensed under the MIT License - see the LICENSE file for details.
👥 Contributing
Contributions are welcome! Please feel free to submit a Pull Request.

Fork the repository
Create your feature branch (git checkout -b feature/AmazingFeature)
Commit your changes (git commit -m 'Add some AmazingFeature')
Push to the branch (git push origin feature/AmazingFeature)
Open a Pull Request

🙏 Acknowledgements

ESP8266 Community for the excellent board support
Arduino for the programming framework
Original examples from the ESP8266WiFi library
