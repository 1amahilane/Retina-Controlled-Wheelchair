# Retina-Controlled-Wheelchair
A gaze-controlled wheelchair using Python for eye-tracking (via the GazeTracking library) and an ESP8266 with a motor driver for wireless control.


# Gaze-Controlled Wheelchair 👁️♿

This project is a prototype for a hands-free, gaze-controlled wheelchair. It uses a computer's webcam to track the user's eye movements and wirelessly controls a wheelchair chassis using an ESP8266 as a web server.

## 🚀 Key Features

* **Hands-Free Control:** Navigate the wheelchair simply by looking (left, right, or center).
* **Wireless Operation:** A Python script on a PC sends HTTP requests over Wi-Fi to the ESP8266.
* **Lightweight Server:** The ESP8266 runs a minimal web server to listen for commands.
* **Accessible Tech:** Built with common, low-cost components like an ESP8266, a motor driver, and a standard webcam.

---

## 🛠️ How It Works

The system is split into two parts: the host computer (client) and the wheelchair (server).

### 1. Host Computer (Python Client)

* A Python script runs on a laptop/PC with a webcam.
* It uses the **`GazeTracking`** library to analyze the video feed in real-time.
* Based on the user's gaze ("left", "right", "center"), the script uses the **`requests`** library to send an HTTP GET request to the ESP8266's IP address.
* **Example:** If the user looks left, the script sends a request to `http://<ESP_IP>/left`.

### 2. Wheelchair (ESP8266 Server)

* The ESP8266 is programmed using the **Arduino IDE** and connects to the local Wi-Fi.
* It runs a lightweight web server using the **`ESP8266 TO PY`** micro-library.
* The library's `waitUntilNewReq()` function blocks and waits for a new HTTP request.
* When a request is received (e.g., from `http://<ESP_IP>/left`), the `getPath()` function extracts the path (`/left`).
* A `switch` or `if/else` block in the main loop matches this path to a motor function (e.g., `goLeft()`), which sends the correct signals to the **motor driver**.

---

## 💻 Technology Stack

* **Gaze Tracking:** Python, OpenCV, `GazeTracking` library.
* **Host Client:** Python `requests` library.
* **Microcontroller:** ESP8266 (programmed via the Arduino IDE).
* **Hardware:**
    * Webcam
    * Motor Driver ( L298N)
    * Wheelchair chassis with DC motors
* **Communication Protocol:**
    * **HTTP/TCP:** The ESP8266 acts as a **Wi-Fi server** on port 80. The Python script is the **client**.
    * **REST-like API:** Commands are sent as URL paths (e.g., `/forward`, `/stop`).
    * **Core Library:** `ESP8266 TO PY` (by Junicchi) handles all server and request-parsing logic on the ESP8266.

---


## 🙏 Acknowledgements

* The core gaze-tracking functionality is powered by the **[GazeTracking library](https://github.com/antoinelame/GazeTracking)** by Antoine Lamé.
* The ESP8266 web server logic is handled by the **[ESP8266 TO PY](https://github.com/Kebablord)** micro-library by Junicchi.
