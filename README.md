# GuardX – Smart Anti-Theft System

A compact, low-cost, IoT-enabled anti-theft device designed to protect small personal belongings using motion sensing and RFID/GSR-based owner authentication. GuardX detects unauthorized touch or movement in real time and raises local and optional remote alerts.

---

## Project Overview

GuardX is a lightweight embedded security device built with ESP32 / ESP8266, motion sensors, and RFID/GSR touch sensing. The system compares live sensor inputs with pre-calibrated owner signatures to determine authorized vs. unauthorized interactions.

Key capabilities:
- Real-time detection of lifting, tilting, or displacement
- Owner verification using RFID + GSR touch sensing
- Immediate buzzer alerts and optional IoT notifications (Blynk, MQTT, Firebase)
- Low-power operation for portable items

---

## Features

- Smart motion detection (lift, tilt, displacement)
- RFID/GSR-based biometric-style owner verification
- Instant buzzer alerts for unauthorized access
- Optional push notifications via Blynk, MQTT, or Firebase
- Compact, battery-powered hardware design
- No computer vision or ML required
- Ideal for hostels, dorms, offices, and travel

---

## Hardware Requirements

- ESP32 or ESP8266 microcontroller
- MPU6050 (or similar) accelerometer/gyro sensor
- RFID RC522 reader and tags OR a GSR touch sensor
- Buzzer and LEDs for local alerts/status
- Li-ion battery (or 9V) and power management components
- Jumper wires, breadboard or custom PCB

---

## System Architecture

For a clean visual, place the architecture diagram in docs/architecture.png and the wiring in schematics/circuit.png.

- System architecture image: docs/architecture.png
- Wiring / circuit diagram: schematics/circuit.png

If the images are present, they will render in GitHub automatically. Example inline usage:
![System Architecture](docs/architecture.png)

---

## Project Structure

GuardX/
- firmware/ — Core device firmware (ESP32/ESP8266)
  - guardx_main.ino — Main program logic
  - gsr_rfid_module.h — GSR/RFID owner authentication module
  - motion_detection.h — Accelerometer / motion detection logic
  - alerts.h — Buzzer + IoT alert functions
- schematics/ — Hardware reference files
  - circuit.png — Circuit wiring diagram
  - block_diagram.png — System block diagram
- docs/ — Documentation assets
  - architecture.png — System architecture flow
  - flowchart.png — Runtime flowchart
  - usecase.png — Use-case diagram
- data/ — Sensor readings (authorized/unauthorized)
  - readings.csv — Raw calibration / test data
- utils/ — Helper scripts and tools
  - calibration_tool.py — Touch/motion calibration script
  - analyzer.py — Motion + GSR data analysis
- mobile/ — IoT notification integration docs
  - blynk_setup.md — Blynk setup guide
  - mqtt_config.md — MQTT configuration guide
- .env.example — Template for IoT API keys (do not commit secrets)
- .gitignore — Ignore firmware builds & secrets
- package.json — (optional) web dashboard / IoT UI
- README.md — This documentation

---

## Installation & Setup

1. Clone the repository:
   ```
   git clone https://github.com/your-username/GuardX.git
   cd GuardX
   ```

2. Install required Arduino libraries (via Library Manager or PlatformIO):
   - MFRC522 (if using RC522 RFID)
   - MPU6050 / Adafruit Sensor or equivalent
   - Blynk (optional) / PubSubClient (MQTT) / Firebase libs (optional)
   - WiFi.h, Wire.h, and other core Arduino libs

3. Configure environment (create a local `.env` from `.env.example` if using IoT integrations):
   - MQTT broker URL, username, password
   - Blynk auth token
   - Any push notification keys (Firebase, etc.)

4. Flash firmware:
   - Open `firmware/guardx_main.ino` in Arduino IDE (or import with PlatformIO)
   - Select the correct board (ESP32/ESP8266) and port
   - Compile and upload

---

## How the System Works (High level)

1. System Arming
   - Owner leaves the item; system records baseline motion values and owner touch signature (GSR/RFID).

2. Touch Detection
   - When touch is detected:
     - If touch matches owner signature → system remains in Safe mode.
     - If touch does not match → system enters Warning/Alert state.

3. Movement Detection
   - Motion events (lift, tilt, displacement) are compared against threshold values.
   - If motion occurs and no owner is verified → Alarm triggered.

4. Alerting
   - Local: buzzer and LEDs
   - Remote (optional): MQTT / Blynk / Firebase push notification

---

## Testing & Validation

| Test Case                        | Expected Output |
|----------------------------------|-----------------|
| Owner touches item               | No alert        |
| Owner lifts item                 | No alert        |
| Unauthorized person touches item | Warning alert   |
| Unauthorized lifts item          | Full alarm      |
| Light vibrations                 | Ignored         |
| Tilt above threshold             | Alarm           |

Tips:
- Use `utils/calibration_tool.py` to tune motion and GSR thresholds.
- Capture traces to `data/readings.csv` for repeatable tests.

---

## Scope & Limitations

Scope:
- Real-time motion + RFID/GSR owner verification
- Low-cost, battery-powered prototype
- Immediate alerts via buzzer and optional IoT notification

Limitations:
- GSR readings can vary with humidity/sweat
- Single authorized user by default
- Intended for indoor/personal items (no GPS/location)
- Not suitable for industrial asset tracking

---

## Future Enhancements

- GPS add-on for outdoor tracking
- Multiple authorized users
- Ultra-low-power deep-sleep modes
- Full Android/iOS companion app
- Smart lock / actuator integration

---

## License

This project is released under the MIT License. Add a LICENSE file at the repository root.

---

## Contributors

- ARSHITHA MS  
- SHAIK SAMREEN

---

