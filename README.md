# GuardX – Smart Anti-Theft System

A compact, low-cost, IoT-enabled anti-theft device designed to protect small personal belongings using motion sensing and RFID/GSR-based owner authentication. GuardX prevents theft in real time by detecting unauthorized touch or movement.

---

## Project Overview

GuardX is a lightweight embedded security device built using ESP32/ESP8266, motion sensors, and RFID/GSR touch sensing.  
The system identifies unauthorized handling by comparing real-time sensor inputs with pre-calibrated owner signatures.

It provides:

- Real-time detection of lifting, tilting, or movement  
- Owner authentication using RFID/GSR touch sensing  
- Immediate alarms and optional IoT notifications  
- Low-power operation suitable for small portable items  

---

## Features

- Smart motion detection (lift, tilt, displacement)  
- RFID/GSR-based biometric-style owner verification  
- Instant buzzer alerts for unauthorized access  
- Optional IoT push notifications (Blynk/MQTT/Firebase)  
- Compact and battery-powered hardware design  
- No machine learning or image processing required  
- Ideal for hostels, dorms, offices, and travel use  

---

## Hardware Requirements

- ESP32 / ESP8266 microcontroller  
- MPU6050 or Tilt/Accelerometer sensor  
- RFID RC522 or GSR touch sensor  
- Buzzer for alarm  
- LEDs for system indication  
- Li-ion/9V battery  
- Jumper wires, breadboard or PCB  

---

## System Architecture

  Owner Touch
        │
 ┌──────▼────────┐
 │ RFID/GSR Auth │
 └──────┬────────┘
        │ Verified / Not Verified
        ▼
┌──────────────────┐
│ Motion Detection │
└──────┬───────────┘
│
▼
┌──────────────────┐
│ Decision Module │
│ (Safe / Alert) │
└──────┬───────────┘
│
Unauthorized?
│ │
No Yes
│ │
Safe Mode Trigger Alarm
│
┌────────▼─────────┐
│ Buzzer + IoT Msg │
└──────────────────┘
## Project Structure
GuardX/
│
├── firmware/
│ ├── guardx_main.ino
│ ├── gsr_rfid_module.h
│ ├── motion_detection.h
│ ├── alerts.h
│
├── schematics/
│ ├── circuit.png
│ ├── block_diagram.png
│
├── docs/
│ ├── architecture.png
│ ├── flowchart.png
│ ├── usecase.png
│
└── README.md
## Installation & Setup

### 1. Clone Repository
git clone https://github.com/your-username/GuardX.git

cd GuardX

### 2. Install Arduino Libraries
- MFRC522 (if using RFID)  
- MPU6050 / Adafruit Sensor  
- Blynk / MQTT / Firebase (optional)  
- WiFi.h  
- Wire.h  

### 3. Flash Code  
Upload `guardx_main.ino` to ESP32/ESP8266 using Arduino IDE.

---

## How the System Works

### 1. System Armed
- Owner leaves the item  
- Baseline motion values recorded  
- GSR/RFID owner touch value stored  

### 2. Touch Detected
- If touch matches owner → safe  
- If mismatch → unauthorized touch alert  

### 3. Movement Detected
- Lift, tilt, motion triggers event  
- If owner is absent → alarm + optional notification  

### 4. Alert Mechanism
- Buzzer beeps continuously  
- IoT platform notifies owner instantly  

---

## Testing & Validation

| Test Case                        | Expected Output |
| -------------------------------- | --------------- |
| Owner touches item               | No alert        |
| Owner lifts item                 | No alert        |
| Unauthorized person touches item | Warning alert   |
| Unauthorized lifts item          | Full alarm      |
| Light vibrations                 | Ignored         |
| High tilt > threshold            | Alarm           |

---

## Scope of the Project

### Scope
- Develop a compact, low-cost theft-prevention device  
- Implement real-time motion + GSR/RFID-based detection  
- Improve ownership verification accuracy  
- Provide instant alerts using IoT platforms  

### Target Audience
- Hostel students  
- Office users  
- Travellers  
- Users carrying wallets, keys, bags, jewellery, gadgets  

### Deliverables
- Fully working hardware prototype  
- Mobile/IoT dashboard for alerts  
- Documentation (design, setup, analysis)  

### Inclusions
- Motion + GSR/RFID sensor integration  
- Embedded C firmware  
- IoT alert workflow  
- Indoor theft-prevention testing  

### Exclusions
- No GPS outdoor tracking  
- No high-end biometrics  
- No video/image-based AI  
- Not for industrial assets  

### Data
- Real-time sensor readings labelled as “authorized/unauthorized”  
- Baseline calibration of owner GSR/RFID values  
- Noise filtering + normalization  

### Limitations
- GSR may vary with sweat/humidity  
- Single authorized user in this version  
- Indoor-only system  
- Sensitivity changes with item type  

---

## Future Enhancements

- GPS add-on for outdoor tracking  
- Multiple authorized users  
- Ultra-low power mode  
- Full Android/iOS app  
- Smart lock integration  

---

## License
MIT License.

---

## Contributors
1.ARSHITHA MS
2.SHAIK SAMREEN 

