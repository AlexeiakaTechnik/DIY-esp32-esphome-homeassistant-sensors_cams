# Engineering of DIY Esp32 Temperature, Humidity and CO2 Esphome Sensors and Esp32 Cameras for use in Home Assisant
Article about my DIY Project to engineer and use esp32 based Temperature, Humidity, CO2 sensors and esp32 Cameras with esphome for Home Assistant. Design(Autocad Inventor), 3d printing, wiring, design flaws and itertions, configuration, calibration description. Thoughts and conclusions on DIY IOT(Internet of Things) devices and how they differ in hands-on experience from commercial products. Learning experience.

# Engineering DIY ESP32 Sensors & Cameras for Home Assistant

## Overview
This article documents the full journey of building DIY ESP32-based smart sensors and cameras for use with Home Assistant (HA). It combines 3D design, prototyping, wiring, firmware configuration, calibration, and final integration into a robust local-first smart home system. 

This project showcases a deep-dive into technical implementation, creativity, and troubleshooting, using affordable parts to create real, useful, and elegant devices — all documented with photos, videos, graphs, and YAML configs.

---

## 1. Motivation & Goals
Commercial devices are often overpriced, cloud-dependent, or offer limited flexibility. DIY devices, while more effort, offer ultimate control, better privacy, and an opportunity to truly learn the internals of smart home automation.

**Project Goals:**
- Build working sensors for temperature, humidity, CO₂
- Design and print durable, aesthetic 3D cases
- Integrate into Home Assistant dashboards
- Tune and calibrate devices for accuracy
- Bonus: Build ESP32-based cameras with local RTSP streaming

---

## 2. Hardware
### Microcontroller:
- ESP32-S3 WROOM-1 Dev Board (Wi-Fi + USB-C)

### Sensors:
- SCD41 (CO₂, Temp, Humid)
- DHT20 / AHT21 (Temperature & Humidity for simpler builds)

### Cameras:
- ESP32-CAM modules with OV2640

---

## 3. 3D Design in Autodesk Inventor
- **Version 1:** Initial print failed due to poor ventilation → photos + lessons learned
- **Version 2:** Redesigned casing with better airflow, mounting slots, and compact layout
- 3D STL files available in repo

---

## 4. Assembly & Wiring
- Step-by-step wiring diagrams and photos
- Power: USB-C or screw terminal
- ESPHome YAML includes pin mappings and sensor config

---

## 5. YAML Configuration (ESPHome)
```yaml
esphome:
  name: esp32-sensor-co2
  platform: ESP32
  board: esp32dev

sensor:
  - platform: scd4x
    co2:
      name: "Living Room CO₂"
    temperature:
      name: "Living Room Temperature"
    humidity:
      name: "Living Room Humidity"
    update_interval: 60s
```
Includes voltage sensor, uptime, signal strength, OTA configs, etc.

---

## 6. Calibration
- Compared readings with digital thermometers and hygrometers
- Measured offsets over time, applied linear/non-linear correction
- Used spreadsheet to graph real vs measured temperature → correction factor derived

```yaml
sensor:
  - platform: template
    name: "Corrected Temperature"
    lambda: |-
      return (x - 1.7);  # basic linear offset
```

---

## 7. Integration with Home Assistant
- Integrated via ESPHome native API
- Entity names standardized for clarity (e.g., `sensor.living_room_co2`)
- Used in:
  - Dashboard badges & cards
  - Alarm triggers
  - Automation for ventilation/humidification

---

## 8. UI & Dashboards
- Designed dashboards for **tablets** and **mobile phones** (portrait + landscape)
- Devices added to room views, gauge cards, graphs
- Bonus: CO₂ LED alert on sensor body for quick glance
- Linked dashboard repo: [Home Assistant Dashboards](https://github.com/AlexeiakaTechnik/Practial-and-stylish-Home-Assistant-Dashboards-for-Tablets-and-Mobile-Phones)

---

## 9. Final Build & Use
- Final assembled sensors labeled with stickers: name, IP, MAC, function
- Mounted in various rooms with 3M backing or screws
- Monitored daily via HA and graphs

---

## 10. Bonus – ESP32 Cameras
- ESP32-CAM modules set up with motion detection and streaming
- RTSP stream integrated into HA Lovelace dashboard
- Stored SD recordings (motion-based)
- Future improvements: add PIR sensor or IR LED for night vision

---

## Media Gallery
✅ Photos of all steps: CAD, printing, wiring, dashboards  
✅ Video of finished sensors & camera in use  
📂 [Google Drive Media Folder](https://drive.google.com/drive/folders/your-real-link-here)

---

## Related Articles
- [AJAX Alarm Integration](https://github.com/AlexeiakaTechnik/AJAX_security-integration-in-Home_Assistant)
- [Light Automation UX](https://github.com/AlexeiakaTechnik/My-experience-of-improving-Light-Automations-in-Home-Assistant)
- [HA UI/Dashboards](https://github.com/AlexeiakaTechnik/Practial-and-stylish-Home-Assistant-Dashboards-for-Tablets-and-Mobile-Phones)

---

## Final Thoughts
This was an intense but rewarding project. I built something real, tangible, and useful for my smart home with the skills to replicate and expand it anytime. I hope it inspires others to build, improve, and learn. Reach out if you want to collaborate, or have questions!
