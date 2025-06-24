
# Engineering DIY ESP32 Sensors & Cameras for Home Assistant
Article about my DIY Project to engineer and use esp32 based Temperature, Humidity, CO2 sensors and Cameras with esphome for Home Assistant. Design(Autocad Inventor), 3d printing, wiring, design flaws and itertions, configuration, calibration description. Thoughts and conclusions on DIY IOT(Internet of Things) devices and how they differ in hands-on experience(and final price) from commercial products.



## Overview
This article documents the full journey of building DIY ESP32-based smart sensors and cameras for use with Home Assistant (HA). It combines 3D design, prototyping, wiring, firmware configuration, calibration, and final integration into a robust local-first smart home system. 

This project showcases a deep-dive into technical implementation, creativity, and troubleshooting, using affordable parts to create real, useful, and elegant devices — all documented with photos, videos, graphs, and YAML configs.

---

## 1. Motivation & Goals
I have to be honest, firt thing that really picked my inerest while resarching esp32 devices, esphome is very cheap-priced parts from Aliexpress. Why buy a [brand](https://aliexpress.ru/item/1005004716755040.html?sku_id=12000030213503813&spm=a2g2w.productlist.search_results.0.290a1bb7HElnHT) [devices](https://aliexpress.ru/item/1005007201324957.html?sku_id=12000039786855672&spm=a2g2w.productlist.search_results.8.290a1bb7HElnHT) when you can seemingly easily do it yourself with [cheap](https://aliexpress.ru/item/1005005501298967.html?spm=a2g2w.orderdetail.0.0.4c7137d4TnwiZl&sku_id=12000039876819440&_ga=2.230843423.1283486305.1750753652-1749897236.1735401406) [available](https://aliexpress.ru/item/33037061522.html?spm=a2g2w.orderdetail.0.0.4c1937d4itn8ht&sku_id=12000032670222591&_ga=2.230843423.1283486305.1750753652-1749897236.1735401406) parts? Then I thought maybe it will be a good learning and practice experience. Then it got more compllicated and.. insightfull. Else - commercial devices are often overpriced, cloud-dependent, or offer limited flexibility. DIY devices, while more effort, offer ultimate control, better privacy, and an opportunity to truly learn the internals of smart home automation.

**Project Goals:**
- Build working sensors for temperature, humidity, CO₂
- Design and print durable, aesthetic 3D cases
- Integrate into Home Assistant dashboards
- Tune and calibrate devices for accuracy
- Bonus: Build ESP32-based cameras with local RTSP streaming

---

## 2. Hardware
### Microcontroller:
- ESP32-S3 WROOM-1 Dev Board (Wi-Fi + USB-C) [Link](https://aliexpress.ru/item/1005005501298967.html?spm=a2g2w.orderdetail.0.0.4c7137d4TnwiZl&sku_id=12000039876819440&_ga=2.230843423.1283486305.1750753652-1749897236.1735401406)
![esp32 s3 dev board ali](https://github.com/user-attachments/assets/af178479-dccb-434f-9971-bea8720ae2f3)

### Sensors:
- SCD41 (CO₂, Temp, Humid) [Link](https://aliexpress.ru/item/1005004221715765.html?spm=a2g2w.orderdetail.0.0.126a37d4laEBru&sku_id=12000033355316689&_ga=2.134440049.1283486305.1750753652-1749897236.1735401406)
- DHT22 / AM2302 (Temperature & Humidity for simpler builds) [Link](https://aliexpress.ru/item/33037061522.html?spm=a2g2w.orderdetail.0.0.4c1937d4itn8ht&sku_id=12000032670222591&_ga=2.230843423.1283486305.1750753652-1749897236.1735401406)
![scd41 ali](https://github.com/user-attachments/assets/477ddb7e-7f88-4cf3-ac1e-d5916e2ad93e)
![dht22 ali](https://github.com/user-attachments/assets/ed4c8073-e8a3-40e3-97c6-29cfc198ea19)

### Cameras:
- ESP32-CAM modules with OV2640 [Link](https://aliexpress.ru/item/1005001621697965.html?spm=a2g2w.orderdetail.0.0.6de837d4VH0e7z&sku_id=12000024948767464&_ga=2.134440049.1283486305.1750753652-1749897236.1735401406)

![esp32 cam ali](https://github.com/user-attachments/assets/3583a012-cf5c-44e3-820a-b7b51197d02d)

### Power adapters:
- cheap nonames from aliexpress/joom [Link](https://aliexpress.ru/item/32619537590.html?spm=a2g2w.orderdetail.0.0.451f4aa6zY7UPy&sku_id=10000013194699312&_ga=2.187878568.1283486305.1750753652-1749897236.1735401406)

### Usb cables:
- cheapest you can find, power delivery only [USB-C](https://aliexpress.ru/item/1005007516957301.html?spm=a2g2w.orderdetail.0.0.441037d4I289Gu&sku_id=12000041097922763&_ga=2.134440049.1283486305.1750753652-1749897236.1735401406) [Micro-USB](https://aliexpress.ru/item/1005004295707775.html?spm=a2g2w.orderdetail.0.0.136337d4o0lsj7&sku_id=12000028666353690&_ga=2.227246109.1283486305.1750753652-1749897236.1735401406)

---

## 3. 3D Design in Autodesk Inventor
I decided to approach this thoroughly and arranged a short r&d design and engineering course from my friend, who is seasoned mechanical engineer. Basically to learn begginer things in Autodesk Inventor, how 3d printing works, how to prototype and iterate. Really - you can do all of that online, there are great articles/youtube channels on how to do basic stuff in Inventor, and you can always find someone nearby who will print you your details for a modest price if you provide them with .STEP files from Inventor.

- **Version 1:**
Initial version of devices were super simple and as you can see on pictures below(I did not see at the moment somehow) they had glaring.. heat dispersion issues. That small grill in front could do little to prevent heat transfer from esp32 chip and onboard LEDs to actual DHT22/SCD41 sensors. I had to learn it the hard way so maybe you dont have to. 
*esp32 Cameras on the other hand were designed kind of ok, but still they were getting too warm and added some more ventilaion in v2.

- **First I created the board, sensors and esp32 cams Inventor 3d models using caliper to take measurements:
**
Esp32 S3 Dev board:
![Inventor - esp32 dev board](https://github.com/user-attachments/assets/c4cf87f9-73df-47ff-bd0c-d35ac12d8e04)

DHT22 Sensor:
![Inventor - temp humid sensor WIP 3](https://github.com/user-attachments/assets/528a5734-43da-4d1c-a023-ee7ecd691933)

SCD41 Sensor:
![Inventor - csd41](https://github.com/user-attachments/assets/6edcbdb8-f27a-4e1c-923f-fcefdbc7e079)

Esp32 Cam with Antenna and fastening washers:
![Inventor - esp32 Cam](https://github.com/user-attachments/assets/112a970c-9815-410f-aa66-717a4cb78e13)

This step in a necessary to do if you want to make sure evrything fits well together during the assembly in Inventor, when you will create cases for devices!

![Inventor - esp32 Cam 2](https://github.com/user-attachments/assets/f59eefa5-be90-4ab8-958a-7f8699cde694)![Inventor - esp32 Cam 3](https://github.com/user-attachments/assets/bbf0a26f-ddb2-472e-85b1-7bc96fada4aa)

- **Secondly I have created the cases for the devices:
**

Case for Esp32 S3 Dev Board, for both Temperature and Humidity(DHT22) and CO2/Temp/Humid(SCD41) devices:
![Inventor - case esp32 dev board v1](https://github.com/user-attachments/assets/c23f5c62-74f6-4f5c-a5f1-956ab9be8506)

Lids for both sensor devices:
![Inventor - lids for sensors v1](https://github.com/user-attachments/assets/8f4ac382-0bc1-4424-aa97-ef648e9903fb)

Case for Esp32 Camera:
![Inventor - case esp32 cam v1](https://github.com/user-attachments/assets/f7fc1eb0-0fcf-4c06-b1b2-61832f9feb74)

- **Finally - Assebly of all devices in Inventor and saving to .STEP format for 3D Printing:
**

Temperature and Humidity(DHT22) and CO2/Temp/Humid(SCD41):
![Inventor - co2 and temp-humid sensors assembly v1](https://github.com/user-attachments/assets/7a121242-755c-4cfd-811f-2f90f7c8fe3f)

Esp32 Camera:

![Inventor - esp32 cam assembly v1](https://github.com/user-attachments/assets/a07e27b5-f7dd-4b86-ab58-2eba2bfa0bcc)

- **3D Prinitng was done on Creality Ender-3 printer, 3d printing instructions(G-Code) were compied in Prusa Slicer software:
**

3D Printer:
![3d Printer 1](https://github.com/user-attachments/assets/c7aee7a1-e17e-4cc5-8f2a-027130a86b08)

Prusa Slicer:
![image](https://github.com/user-attachments/assets/6a69a610-47d4-4cbe-8d86-31197c2108db)

- **Assembly, first run and conclusions:**

After soldiering wires, physical assembly, esphome configuration upload and a few tests I quickly realized the grave mistake of heat dispersion problem for sensors. Esp32 Cam was basically ok, but come summer - I was sure it would overheat and start to freeze/glitch.

![image](https://github.com/user-attachments/assets/2ce4a40c-bdec-4fdf-9068-fe31039e465b)
![image](https://github.com/user-attachments/assets/f82488f1-c9da-41de-94a6-17d192137aab)


- **Version 2:** Redesigned casing with better airflow, mounting slots, and compact layout
- 3D STL files available in repo


ou

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
