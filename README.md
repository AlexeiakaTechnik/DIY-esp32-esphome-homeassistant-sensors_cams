![All Sensors - Work desk 1](https://github.com/user-attachments/assets/a0f44efd-c6e8-4914-a172-ff47eea20a60)
# Engineering DIY ESP32 Sensors & Cameras for Home Assistant
Article about my DIY Project to engineer and use esp32 based Temperature, Humidity, CO2 sensors and Cameras with esphome for Home Assistant. Design(Autodesk Inventor), 3d printing, wiring, design flaws and itertions, configuration, calibration description. Thoughts and conclusions on DIY IOT(Internet of Things) devices and how they differ in hands-on experience(and final price) from commercial products.



## Overview
This article documents the full journey of building DIY ESP32-based smart sensors and cameras for use with Home Assistant (HA). It combines 3D design, prototyping, wiring, firmware configuration, calibration, and final integration into a robust local-first smart home system. 

This project showcases a deep-dive into technical implementation, creativity, and troubleshooting, using affordable parts to create real, useful, and elegant devices — all documented with photos, videos, graphs, and YAML configs.

---

## 1. Motivation & Goals
I have to be honest, firt thing that really picked my inerest while resarching esp32 devices, esphome is very cheap-priced parts from Aliexpress. Why buy a [brand](https://aliexpress.ru/item/1005004716755040.html?sku_id=12000030213503813&spm=a2g2w.productlist.search_results.0.290a1bb7HElnHT) [devices](https://aliexpress.ru/item/1005007201324957.html?sku_id=12000039786855672&spm=a2g2w.productlist.search_results.8.290a1bb7HElnHT) when you can seemingly easily do it yourself with [cheap](https://aliexpress.ru/item/1005005501298967.html?spm=a2g2w.orderdetail.0.0.4c7137d4TnwiZl&sku_id=12000039876819440&_ga=2.230843423.1283486305.1750753652-1749897236.1735401406) [available](https://aliexpress.ru/item/33037061522.html?spm=a2g2w.orderdetail.0.0.4c1937d4itn8ht&sku_id=12000032670222591&_ga=2.230843423.1283486305.1750753652-1749897236.1735401406) parts? Then I thought maybe it will be a good learning and practice experience. Then it got more compllicated and.. insightfull. Additionally - I considered that commercial devices are often overpriced, cloud-dependent, or offer limited flexibility. DIY devices, while more effort, offer ultimate control, better privacy, and an opportunity to truly learn the internals of smart home automation.

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

## 3.1. First Iteration
- **Version 1:**
Initial version of devices were super simple and as you can see on pictures below(I did not see at the moment somehow) they had glaring.. heat dispersion issues. That small grill in front could do little to prevent heat transfer from esp32 chip and onboard LEDs to actual DHT22/SCD41 sensors. I had to learn it the hard way so maybe you dont have to. 

*esp32 Cameras on the other hand were designed kind of ok, there isn't much to it, but still they were getting too warm.

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

After soldiering wires, physical assembly, esphome configuration upload and a few tests I quickly realized the grave mistake of heat dispersion problem for sensors. Sensor temperature readings were about 5-8(!) degrees celcius above readings from lab thermometer I placed beside. Esp32 Cam was basically ok, but come summer - I was sure it would overheat and start to freeze/glitch.

![image](https://github.com/user-attachments/assets/2ce4a40c-bdec-4fdf-9068-fe31039e465b)
![image](https://github.com/user-attachments/assets/f82488f1-c9da-41de-94a6-17d192137aab)

## 3.2. Second Iteration
- **Version 2 - Learning from mistakes:** 
I got back to Inventor and redesigned casing with better airflow, mounting slots, compact layout. And added some design elements - Home Assistant logo as a vent! 

*After coming up with "final" version of Esp32 Dev Board Casing(a few attempts) to save up on printing cost I have only redigned Lids for sensor devices, adding external holder for the sensors to distance them from the main board case and added additional lid to enclose the sensor itself. With ALL the extra ventilation grills 3D printer and size allowed for! =)

*Esp32 Cam Casing and Lid only suffered through adding additional vents, some design beuty, and better grip for the board to be able to connect/disconnect micro USB securely.

Temperature and Humidity(DHT22) and CO2/Temp/Humid(SCD41) V2:
![Inventor - co2 and temp-humid sensors assembly v2](https://github.com/user-attachments/assets/17a39c16-7732-4af3-9bf4-814a9f7e4f12)


Esp32 Camera V2:
![Inventor - esp32 cam assembly v2](https://github.com/user-attachments/assets/0de06a3f-8369-4b96-8a8b-ad7f86dc0ee6)


The final print of additional parts:
![case print v2 1](https://github.com/user-attachments/assets/565f3b70-5583-4baf-8d94-9331cbb1952c)


To add flawor and practicality to the design I have ordered some simple stickers to be printed - to identify devices(Device purpose, Room name, Local IP address and esp32 wi-fi module MAC address). On the photo below you can see the whole parade of devices before I replaced casings/lids and redid wiring(now sensors were further apart from esp32 board). 

Devices v1 to v2 reassembly:
![All Sensors - Work desk - before reassembly v1 to v2](https://github.com/user-attachments/assets/96234ae3-fa14-44ff-a5f0-e1b80008c5b5)

The "final", albeit final for this article, design of Sensors and Cameras:
![All Sensors - Work desk - final v2 assembled](https://github.com/user-attachments/assets/c6dd6aac-e4ce-4845-bf59-cd2384670b6e)

- **Version 2 - Results:**
The heating dispersion problem got much better. From +5-8 degrees I got to +2-3 for temperature readings. It's still critical for including such sensors in climate automations but now its something which actually can be calibrated - we will get to in **chapter 6**. The design additions were a surprising delight, considering that now esp32 dev board built-in RGB LEDs can be used to do some visual aid as explained in **chapter 7**. Of course the design of such devices can be improved million times over but for the purpose of this article I decided to stop and actually try using them in real Smart Home conditions. As the professional engineer buddy of mine(who helped with making sense of Inventor and how to r&d 101) explained: 


_"There is no perfect design for an engineer, do not get lost in drawing and re-drawing lots of blueprints, trying to **think of every detail and aspect in theory**. Try out your designes, fail miserably, get back to board, try againm, fail less... Only then **you will actually make progress**. Through prototyping and iterations."_


## 4. Assembly, Wiring and Hardware specifics
- **Temperature and Humidity(DHT22) and CO2/Temp/Humid(SCD41) devices:** 
The wiring is really simple for this project. For the **DHT22** sensor - it only has 3 pins: **plus(3.3V)** **ground(-3.3V)** and **Output(Out)**. So any (GRND) pin from esp32 board connects to sensors ground, any 3.3V pin from board to (+) and any numbered pin, which is not specifically stated for other purposes in this board's documentation can be connected to sensor's (Out). I have connected (Out) with **GPIO4**. 

Like this(yeah not a clean soldiering but it does its job):
![Wiring - DHT22 Temp Humid Device](https://github.com/user-attachments/assets/f227a2a9-2204-438f-bf62-832ceb689c9e)


- For **SCD41** sensor there are 4 pins: **plus 3.3V(VCC)**, **minus 3.3V(GND)**, **Serial Clock Line(SCL)** - carries the clock signal generated by the master (ESP32) to sync communication and **Serial Data Line(SDA)** - transfers actual data between master (ESP32) and slave device (SCD41 sensor). The VCC and GND pins are obviously wired the same as with DHT22 sensor and SCL / SDA pins are _usually_ connected to common ESP32 I²C(Inter-Integrated Circuit - in simple terms it's a shared bus for communications with electronic components over two lines) Default Pins: **SDA** <=> **GPIO21** and **SCL** <=> **GPIO22**. I have connected them to **GPIO8** and **GPIO9** accordingly.


Like this:
![Wiring - SCD41 CO2-Temp-Humid Device](https://github.com/user-attachments/assets/8315835f-c1f5-480f-be3e-6aab5b028033)


- **Esp32 Camera devices:** 
Those came in sets, as seen in image in **Hardware (#2) Chapter** with already prebuilt set for Camera bus board to be connected to Esp32-S board and wired Antenna. So no additional wiring was required and only the casing to be built around it.

- **Hardware specifications and thoughts:** 
The hardware is simple, requires 5V power, has usually USB-C/Micro ports. Esp32 bpards have signal LEDs(power on, firmware flash/writing to memory), RGB LED - can be used extensively and Reset/Boot buttons. Esp32 Cameras(I have OV2640) are fragile, small-frame and limited in there resolution/quality, but can be replaced with more serious counterparts.

There is a really, _really_ imoprtant critical note here!!! Do not buy cheap-ass ESP32 dev boards unless you want to go down a rabbit hole of guessing pinouts and missing documentation. If it costs under $4, something’s wrong — make sure it’s an original board. Example - Espressif(I got it's knock off): almost $20 to my address [Link](https://aliexpress.ru/item/1005004494348761.html?sku_id=12000032953296653&spm=a2g2w.productlist.search_results.5.5863bc74XreuNA) Trust me, it’s worth the few extra bucks. Oterwise buying cheap components is a lottery. I ended up with 1 defective Esp32 S3 board, 1 fully defective esp32 Cam set and 2 broken DHT22 sensors. 

Other important thing to consider is - those devices require GOOD Wi-Fi signal to operate. Especially if we are talking about Cameras. For the CO2/Temperature/Humidity Sensors it's not that big of a deal, because they dont have to send as much data but for Esp32 Cams you want your Wi-Fi to really reach them. Such cameras are rarely good for full on video security/survailance solutions but are good enogh to put your eyes on something critical - like electrical switchboxes, boilers, solar inverters/batteries/power walls or just kitchens with with fire hazards. 

My initial intent was to use them to monitor exactly such places, but it turned out Wi-Fi signal from basement with Boiler/Washing Machine/Pumps/Controllers was too weak. So if you have thick brick walls or other obstacles - be advised to investigate Wi-Fi signal strength prior to buying!

To be fair, Esp32 Cams are successfully used as with Object detection/recognition systems like [Frigate](https://docs.frigate.video/integrations/home-assistant/) so feel free to experiment.


---

## 5. YAML Configuration (and ESPHome)

ESPHome is a great place to start doing your DIY IOT(Internet Of Things) devices and finding custom approaches to unussual Smart Home challanges. As stated on their [web-site](https://esphome.io/):
_"ESPHome is an open-source firmware framework that simplifies the process of creating custom firmware for popular WiFi-enabled microcontrollers"_ 

ESPHome integrates perfectly with Home Assistant, it uses ESPHome Device Builder Add-on you can add from here:
[![Open this in Home Assistant](https://my.home-assistant.io/badges/supervisor_addon.svg)](https://my.home-assistant.io/redirect/supervisor_addon/?addon=5c53de3b_esphome&repository_url=https%3A%2F%2Fgithub.com%2Fesphome%2Fhome-assistant-addon)

The HA detects through auto-discovery if an ESPHome enabled device appears in your network or you can add it manually via Integration:
[![Open this in Home Assistant](https://my.home-assistant.io/badges/supervisor_addon.svg)](https://my.home-assistant.io/redirect/config_flow_start/?domain=esphome)

To flash ESPHome framework firmware on your device you can either do it from Builder Add-on or use [ESPHome Web](https://web.esphome.io/). Be sure to use usb cable with data transfer line and press (Boot) button if necessary(for most esp32 boards) while connecting to USB port of your computer/HA server. Usually USB Device should be identified as USB JTAG something=something. Take a good look at [ESPHome documentation](https://esphome.io/guides/getting_started_hassio#) for HA, most of things are explained there or Google/ask nearest AI Chatbot for things - they work like a charm!

- **Now let's get down to YAML configuration for our devices:** 

For **Temperature and Humidity(DHT22)** devices I have used following configuration:
```yaml
esphome:
  name: esp32-temphumid-sensor-kitchen
  friendly_name: Home Temp & Humidity Sensor – Kitchen

esp32:
  board: esp32-s3-devkitc-1
  framework:
    type: arduino  # Using Arduino framework for stability and compatibility

# Enable verbose logging via UART
logger:
  level: DEBUG
  baud_rate: 115200  # Default UART speed for serial logging

# Enable API for Home Assistant integration
api:
  encryption:
    key: "REPLACE_WITH_YOUR_API_ENCRYPTION_KEY"
  reboot_timeout: 1min  # Reboot if no API connection for 1 minute
  port: 6053  # Optional, default ESPHome port

# Enable OTA (Over-the-Air) firmware updates
ota:
  - platform: esphome
    password: "REPLACE_WITH_YOUR_OTA_PASSWORD"

# Wi-Fi Configuration
wifi:
  ssid: !secret wifi_ssid         # Use secrets.yaml to protect credentials
  password: !secret wifi_password
  power_save_mode: none           # Better responsiveness
  fast_connect: true              # Skip scanning other networks
  domain: .your-domain.local      # Optional: DNS domain for discovery
  manual_ip:                      # Static IP setup for reliability
    static_ip: 192.168.1.175      # Replace with IP of your choice
    gateway: 192.168.1.1
    subnet: 255.255.255.0
    dns1: 192.168.1.1
    dns2: 8.8.8.8

# Temperature and Humidity Sensor – AM2302 (a DHT22 variant)
sensor:
  - platform: dht
    pin: GPIO4
    model: AM2302
    temperature:
      name: "Kitchen Temperature"
      unit_of_measurement: "°C"
      accuracy_decimals: 1
    humidity:
      name: "Kitchen Humidity"
      unit_of_measurement: "%"
      accuracy_decimals: 1    
    update_interval: 10s  # Refresh every 10 seconds

# Built-in or external RGB LED for status/feedback
light:
  - platform: neopixelbus
    pin: GPIO48
    variant: WS2812          # Popular individually addressable RGB LED
    num_leds: 1              # Single LED
    type: GRB                # Color ordering format
    name: "Sensor RGB LED"
    id: esp32_led
```
For network configuration I strongly reccomend using Static IPv4s, Static DHCP entries(bind device MAC to local IP). If you want a reliable, stress-proof system which will come back from power outages, networking issues/router faults - set as much manually as you can/consider healthy =) For me, with 100+ IoT devices of different sorts/brands/price ranges I had to learn it the hard way. For example I am happily using separate DHCP Server running as [HA Add-on](https://github.com/f18m/ha-addon-dnsmasq-dhcp/tree/main) instead of shitty trimmed-down version found on a lot of consumer=level network equipment - my tp-link as a good example of such case. But maybe you have a great network with Mikrotiks/Ubiquty/PFsense/etc. devices and sys-admin level skills, so you do you.

---

For **CO2/Temp/Humid(SCD41)** devices I have used following configuration:
```yaml

```
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
