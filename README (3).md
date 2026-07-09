# 💧 Personalized Testing Kit for Residual Chlorine in Drinking Water

An IoT-based, low-cost, portable water quality monitoring system that measures **residual chlorine** and **turbidity** in drinking water in real time, displays results locally on an LCD, streams data to the cloud, and sends instant alerts via WhatsApp/Telegram when safe limits are exceeded.

> Mini Project — Department of Electronics and Communication Engineering, Sri Ramakrishna Engineering College, Coimbatore (Anna University) — May 2025
> **Authors:** Pooja Nivethidha M, Preethi B, Priyadharshini H

---

## 🔗 Live Dashboard

📊 **ThingsBoard Dashboard:** [Add your dashboard link here](https://thingsboard.cloud/)

---

## 📸 Project in Action

![Hardware Setup, WhatsApp Alerts & ThingsBoard Dashboard](images/hardware-dashboard-demo.png)

*Left: Real-time turbidity/chlorine alerts received on WhatsApp via Twilio Sandbox.
Top: Breadboard prototype with ESP32, TCS3200 color sensor, SEN0189 turbidity sensor, and I2C LCD.
Bottom: Live ThingsBoard dashboard showing Chlorine (ppm), Turbidity (NTU), and time-series trends.*

---

## 📖 Overview

Access to safe drinking water depends heavily on proper chlorination — too little chlorine fails to disinfect, too much can cause health issues. Traditional testing (lab-based DPD/titration methods) is slow, manual, and impractical for continuous monitoring, especially in rural or resource-limited areas.

This project builds a **compact, battery-powered testing kit** that:
- Detects residual chlorine using **colorimetric analysis** (reagent + color sensor)
- Measures **turbidity** via light-scattering
- Displays live readings on a **16x2 I2C LCD**
- Pushes data to the **cloud (ThingsBoard)** over Wi-Fi using **MQTT**
- Sends **real-time alerts** via WhatsApp/Telegram when thresholds are breached

---

## ⚙️ How It Works

1. A water sample is mixed with an **orthotolidine reagent**, producing a color change proportional to chlorine concentration.
2. The **TCS3200 color sensor** reads the color intensity; the **SEN0189 turbidity sensor** measures light scattering from suspended particles.
3. The **ESP32** microcontroller reads both sensors, applies calibration, and computes chlorine (ppm) and turbidity (NTU) values.
4. Results are shown instantly on the onboard **LCD**.
5. Data is published via **MQTT** to **ThingsBoard**, where it's logged, charted, and visualized on a dashboard.
6. If chlorine or turbidity exceeds safe thresholds, an **alert is triggered** and pushed to the user via WhatsApp/Telegram.

```
Add Reagent → Read Sensors (Color + Turbidity) → Process & Calibrate
     → Send via MQTT to ThingsBoard → Check Thresholds
         ├── Safe → Continue Monitoring
         └── Unsafe → Send Alert (WhatsApp/Telegram/SMS) → Log to Dashboard
```

---

## 🔧 Hardware Components

| Component | Purpose |
|---|---|
| **ESP32 (WROOM-32)** | Central microcontroller — sensor processing + Wi-Fi/MQTT communication |
| **TCS3200 Color Sensor** | Detects color change from chlorine-reagent reaction |
| **SEN0189 Turbidity Sensor** | Measures water clarity (0–1000 NTU) |
| **16x2 I2C LCD** | Local real-time display of readings |
| **Power Supply Unit** | 5V/3.3V regulated supply, portable (Li-ion/Li-Po battery) |
| **LED/Buzzer** | Local visual/audible alert indicator |

---

## 💻 Software Stack

- **Firmware:** MicroPython, written and flashed via **Thonny IDE**
- **Cloud Platform:** [ThingsBoard](https://thingsboard.cloud/) (MQTT-based telemetry, dashboards, alarms)
- **Messaging/Alerts:** Twilio WhatsApp Sandbox / Telegram Bot API
- **Protocol:** MQTT (`v1/devices/me/telemetry`)

---

## 📊 Dashboard Features

- Live **time-series chart** of chlorine & turbidity
- **Gauge widgets** for at-a-glance readings
- **Alarm log** for threshold breaches
- Accessible via web or mobile, anywhere with internet access

---

## 🚀 Getting Started

### Prerequisites
- ESP32 dev board
- TCS3200 & SEN0189 sensors
- 16x2 I2C LCD
- [Thonny IDE](https://thonny.org/) with MicroPython firmware flashed to ESP32
- A [ThingsBoard Cloud](https://thingsboard.cloud/) account and device access token

### Setup
1. Wire the sensors and LCD to the ESP32 as per the pin configuration in [`code.py`](./code.py):
   - Turbidity sensor → ADC Pin 34
   - Color sensor S2/S3 → Pins 25/26, OUT → Pin 27
   - LED → Pin 2
2. Update the Wi-Fi and ThingsBoard credentials in the script:
   ```python
   WIFI_SSID = "your_wifi_name"
   WIFI_PASSWORD = "your_wifi_password"
   THINGSBOARD_TOKEN = "your_device_token"
   ```
3. Flash the script to the ESP32 via Thonny IDE and run.
4. Watch live values in the Thonny shell, on the LCD, and on your ThingsBoard dashboard.
5. Configure alarm rules in ThingsBoard and connect a WhatsApp/Telegram bot for real-time alerts.

---

## ✨ Key Features

- ✅ Real-time, dual-parameter monitoring (chlorine + turbidity)
- ✅ Low-cost, compact, and portable — ideal for households and rural communities
- ✅ Cloud connectivity for remote access and historical trend analysis
- ✅ Instant WhatsApp/Telegram alerts on unsafe readings
- ✅ No lab equipment or trained personnel required

## 🧪 Tested Range

- Chlorine: 0.1 – 5.0 mg/L
- Turbidity: 0 – 1000 NTU

---

## 🔭 Future Enhancements

- Add pH, dissolved oxygen, and conductivity sensors
- Machine learning–based contamination trend prediction
- LoRaWAN support for remote/rural connectivity without Wi-Fi
- Multilingual mobile app interface
- Rugged, waterproof enclosure for field deployment

---

## 📚 References

Full literature survey and citation list available in the [project report](./MP.pdf).

---

## 📄 License

This project was developed as an academic Mini Project (20EC279) at Sri Ramakrishna Engineering College, Coimbatore, under Anna University, Chennai. Feel free to fork and build upon it for educational purposes.
