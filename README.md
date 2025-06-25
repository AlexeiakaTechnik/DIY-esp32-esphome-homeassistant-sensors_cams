![All Sensors - Work desk 1](https://github.com/user-attachments/assets/a0f44efd-c6e8-4914-a172-ff47eea20a60)
# Engineering DIY ESP32 Sensors & Cameras for Home Assistant
Article about my DIY Project to engineer and use ESP32 based Temperature, Humidity, CO2 sensors and Cameras with ESPHome framework for Home Assistant. Design(Autodesk Inventor), 3D printing, wiring, learning design flaws, iterating, configuring and calibrating is explained. Thoughts and conclusions on DIY IOT(Internet of Things) devices and how they differ in hands-on experience(and price) from commercial products.



## Overview
## 📖 Table of Contents

1. [💡 Motivation & Goals](#1-motivation--goals)  
2. [🔩 Hardware](#2-hardware)  
3. [📐 3D Design in Autodesk Inventor](#3-3d-design-in-autodesk-inventor)  
   - [🔁 First Iteration](#31-first-iteration)  
   - [🔁 Second Iteration](#32-second-iteration)  
4. [🔧 Assembly, Wiring and Hardware Specifics](#4-assembly-wiring-and-hardware-specifics)  
5. [📜 YAML Configuration (ESPHome)](#5-yaml-configuration-esphome)  
6. [⚖️ Calibration](#6-calibration)  
7. [🏠 Integration with Home Assistant](#7-integration-with-home-assistant)  
8. [🖥️ UI & Dashboards](#8-ui--dashboards)  
9. [🌈 Bonus – Visual CO₂ Indicator with RGB LED](#9-bonus--visual-co2-indicator-with-rgb-led)  
10. [💬 Final Thoughts](#10-final-thoughts)  
11. [📚 Related Articles](#11-related-articles)

---
This article documents the full journey of building DIY ESP32-based smart sensors and cameras for use with Home Assistant (HA). It combines 3D design, prototyping, wiring, firmware configuration, calibration, and final integration into a robust local-first smart home system. 

This project showcases a deep-dive into technical implementation, creativity, and troubleshooting, using affordable parts to create real, useful, and elegant devices — all documented with photos, videos, graphs, and YAML configs.

---

## 1. 💡 Motivation & Goals
I have to be honest, firt thing that really picked my inerest while resarching ESP32 devices and ESPHome system are very cheap-priced parts from Aliexpress. Why buy [brand](https://aliexpress.ru/item/1005004716755040.html?sku_id=12000030213503813&spm=a2g2w.productlist.search_results.0.290a1bb7HElnHT) [devices](https://aliexpress.ru/item/1005007201324957.html?sku_id=12000039786855672&spm=a2g2w.productlist.search_results.8.290a1bb7HElnHT) when you can, easily do it yourself with [cheap](https://aliexpress.ru/item/1005005501298967.html?spm=a2g2w.orderdetail.0.0.4c7137d4TnwiZl&sku_id=12000039876819440&_ga=2.230843423.1283486305.1750753652-1749897236.1735401406) [available](https://aliexpress.ru/item/33037061522.html?spm=a2g2w.orderdetail.0.0.4c1937d4itn8ht&sku_id=12000032670222591&_ga=2.230843423.1283486305.1750753652-1749897236.1735401406) parts? Or so it seemed like anyway. Then I thought maybe it might be a good learning and practical experience. Then it got more compllicated and.. insightfull. Additionally - I considered that commercial devices are often overpriced, cloud-dependent, or offer limited flexibility. DIY devices, while more effort, offer ultimate control, better privacy, and an opportunity to truly learn the internals of smart home automation.

**Project Goals:**
- Build working sensors for temperature, humidity, CO₂
- Design and print durable, aesthetic 3D cases
- Integrate into Home Assistant dashboards
- Tune and calibrate devices for accuracy
- Bonus: Build ESP32-based cameras with local RTSP streaming for monitoring something at home

---

## 2. 🔩 Hardware
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
- cheap no-names from aliexpress/joom/ebay/whatever [Link](https://aliexpress.ru/item/32619537590.html?spm=a2g2w.orderdetail.0.0.451f4aa6zY7UPy&sku_id=10000013194699312&_ga=2.187878568.1283486305.1750753652-1749897236.1735401406)

### Usb cables:
- cheapest you can find, power delivery only [USB-C](https://aliexpress.ru/item/1005007516957301.html?spm=a2g2w.orderdetail.0.0.441037d4I289Gu&sku_id=12000041097922763&_ga=2.134440049.1283486305.1750753652-1749897236.1735401406) [Micro-USB](https://aliexpress.ru/item/1005004295707775.html?spm=a2g2w.orderdetail.0.0.136337d4o0lsj7&sku_id=12000028666353690&_ga=2.227246109.1283486305.1750753652-1749897236.1735401406)

---

## 3. 📐 3D Design in Autodesk Inventor
I decided to approach this thoroughly and arranged a short r&d/engineering course with my friend, who is a seasoned mechanical engineer. Basically to learn begginer things in Autodesk Inventor, how 3D printing works, how to prototype and test. Really - you can do all of that online, there are great articles/youtube channels on how to do basic stuff in Inventor, and you can always find someone nearby who will print you your details, for a modest price, if you provide them with .STEP/.STM files from Inventor.

### 3.1. 🔁 First Iteration
- **Version 1:**
Initial version of devices was super simple and, as you can see on pictures below(I did not see at the moment somehow), they had a glaring.. heat dispersion issue. That small grill in front could do very little to prevent heat transfer from ESP32 chip and onboard LEDs to DHT22/SCD41 sensors. I had to learn it the hard way, so maybe you dont have to. 

*ESP32 Cameras, on the other hand, were designed kind of ok, there isn't much to it, but still they were getting too warm.

- **First I created the board, sensors and ESP32 Cams Inventor 3D models using caliper to take measurements:**
ESP32 S3 Dev board:
![Inventor - esp32 dev board](https://github.com/user-attachments/assets/c4cf87f9-73df-47ff-bd0c-d35ac12d8e04)

DHT22 Sensor:
![Inventor - temp humid sensor WIP 3](https://github.com/user-attachments/assets/528a5734-43da-4d1c-a023-ee7ecd691933)

SCD41 Sensor:
![Inventor - csd41](https://github.com/user-attachments/assets/6edcbdb8-f27a-4e1c-923f-fcefdbc7e079)

ESP32 Cam with Antenna and fastening washers:
![Inventor - esp32 Cam](https://github.com/user-attachments/assets/112a970c-9815-410f-aa66-717a4cb78e13)

This step in a necessary to do if you want to make sure evrything fits well together during the assembly in Inventor, when you will create cases to enclose the devices!

![Inventor - esp32 Cam 2](https://github.com/user-attachments/assets/f59eefa5-be90-4ab8-958a-7f8699cde694)![Inventor - esp32 Cam 3](https://github.com/user-attachments/assets/bbf0a26f-ddb2-472e-85b1-7bc96fada4aa)

- **Secondly, I have created the cases for the devices:**

Case for ESP32 S3 Dev Board, for both Temperature and Humidity(DHT22) and CO2/Temp/Humid(SCD41) devices:
![Inventor - case esp32 dev board v1](https://github.com/user-attachments/assets/c23f5c62-74f6-4f5c-a5f1-956ab9be8506)

Lids for both sensor devices:
![Inventor - lids for sensors v1](https://github.com/user-attachments/assets/8f4ac382-0bc1-4424-aa97-ef648e9903fb)

Case for ESP32 Camera:
![Inventor - case esp32 cam v1](https://github.com/user-attachments/assets/f7fc1eb0-0fcf-4c06-b1b2-61832f9feb74)

- **Finally - Assembled them in Inventor and saved to .STEP format for 3D Printing:**

Temperature and Humidity(DHT22) and CO2/Temp/Humid(SCD41):
![Inventor - co2 and temp-humid sensors assembly v1](https://github.com/user-attachments/assets/7a121242-755c-4cfd-811f-2f90f7c8fe3f)

ESP32 Camera:

![Inventor - esp32 cam assembly v1](https://github.com/user-attachments/assets/a07e27b5-f7dd-4b86-ab58-2eba2bfa0bcc)

- **3D Prinitng was done on Creality Ender-3 printer, printing instructions(G-Code) were compiled in Prusa Slicer software:**

3D Printer:
![3d Printer 1](https://github.com/user-attachments/assets/c7aee7a1-e17e-4cc5-8f2a-027130a86b08)

Prusa Slicer:
![image](https://github.com/user-attachments/assets/6a69a610-47d4-4cbe-8d86-31197c2108db)

- **Assembly, first run and conclusions:**

After soldering wires, physical assembly, ESPHome configuration upload and a few tests I quickly realized the grave mistake of not providing airflow for the sensors and placing them too close to heat sources. Sensor temperature readings were about 5-8°C(!) above readings from the lab thermometer I placed beside. ESP32 Cam was basically ok, but come summer - I was sure it would overheat and start to freeze/glitch.

![image](https://github.com/user-attachments/assets/2ce4a40c-bdec-4fdf-9068-fe31039e465b)
![image](https://github.com/user-attachments/assets/f82488f1-c9da-41de-94a6-17d192137aab)

### 3.2. 🔁 Second Iteration
- **Version 2 - Learning from mistakes:** 
I got back to Inventor and redesigned casings with better airflow, mounting slots, compact layout. And added some design elements - Home Assistant logo as a vent! 

*After coming up with "final" version of ESP32 Dev Board Casing(a few attempts) - to save up on printing cost, I have only redigned Lids for sensor devices. Added external holder for the sensors to distance them from the main board case and added additional lid to enclose the sensor itself. With ALL the extra ventilation grills 3D printer and size allowed for!

*ESP32 Cam Casing and Lid only suffered through adding vents, some design beauty, and better grip for the board to be able to connect/disconnect micro USB cables securely.

Temperature and Humidity(DHT22) and CO2/Temp/Humid(SCD41) V2:
![Inventor - co2 and temp-humid sensors assembly v2](https://github.com/user-attachments/assets/17a39c16-7732-4af3-9bf4-814a9f7e4f12)


ESP32 Camera V2:
![Inventor - esp32 cam assembly v2](https://github.com/user-attachments/assets/0de06a3f-8369-4b96-8a8b-ad7f86dc0ee6)


The final print of additional parts:
![case print v2 1](https://github.com/user-attachments/assets/565f3b70-5583-4baf-8d94-9331cbb1952c)


To add flawor and practicality to the design, I have ordered some simple stickers to be printed - to identify devices(Function, Room name, Local IP address and ESP32 Wi-Fi module MAC address). On the photo below you can see the whole parade of devices before I replaced casings/lids and redid wiring(now sensors were further apart from ESP32 board pins). 

Devices v1 to v2 reassembly:
![All Sensors - Work desk - before reassembly v1 to v2](https://github.com/user-attachments/assets/96234ae3-fa14-44ff-a5f0-e1b80008c5b5)

The "final", albeit final for this article, design of Sensors and Cameras:
![All Sensors - Work desk - final v2 assembled](https://github.com/user-attachments/assets/c6dd6aac-e4ce-4845-bf59-cd2384670b6e)

- **Version 2 - Results:**
The heating dispersion problem got much better. From +5-8°C degrees I got to +2.8-4.5°C deviation. It is still critical to include such readings in Climate Automation but now it's something which actually can be fixed - we will get to in **[Chapter 6 - Calibration](#6-calibration)**. 

Visual design additions were a surprising delight, considering that now ESP32 dev board built-in RGB LEDs can be used to do some visual aid as explained in **[Visual CO2 Indication Chapter](#9-bonus--visual-co2-indicator-with-rgb-led)**. Of course, functional design of such devices can be improved million times over, but for the purpose of this article I decided to stop and actually try using them in real Smart Home conditions. As the professional engineer buddy of mine(who helped me to make sense of Autodesk Inventor and gave me R&D 101 lessons) explained: 


_"There is no perfect design for an engineer, do not get lost in drawing and re-drawing lots of blueprints, trying to **think of every detail and aspect in theory**. Try out your designes, fail miserably, get back to board, try againm, fail less... Only then **you will actually make progress**. Through prototyping and iterations."_


## 4. 🔧 Assembly, Wiring and Hardware Specifics
- **Temperature and Humidity(DHT22) and CO2/Temp/Humid(SCD41) devices:** 
The wiring is really simple for this project. For the **DHT22** sensor - it only has 3 pins: **plus(3.3V)** **ground(-3.3V)** and **Output(Out)**. So any (GRND) pin from ESP32 board connects to sensor's ground, any 3.3V pin from board to sensor's (+) and any numbered pin, which is not specifically stated to be limited to other purposes in this board's documentation, can be connected to sensor's (Out). I have connected (Out) with **GPIO4**. 

Like this(yeah, not very clean soldering but it does its job):

![Wiring - DHT22 Temp Humid Device](https://github.com/user-attachments/assets/f227a2a9-2204-438f-bf62-832ceb689c9e)


- For **SCD41** sensor there are 4 pins: **plus 3.3V(VCC)**, **minus 3.3V(GND)**, **Serial Clock Line(SCL)** - carries the clock signal generated by the master (ESP32) to sync communication and **Serial Data Line(SDA)** - transfers actual data between master (ESP32) and slave device (SCD41 sensor). The **VCC** and **GND** pins are obvious to be wired the same as with DHT22 sensor and SCL / SDA pins are _usually_ connected to common ESP32 I²C  Default Pins: **SDA** <=> **GPIO21** and **SCL** <=> **GPIO22**. I have connected them to **GPIO8** and **GPIO9** accordingly.

*I²C - Inter-Integrated Circuit - in simple terms it's a shared bus for communications with electronic components over two lines.

Like this:
![Wiring - SCD41 CO2-Temp-Humid Device](https://github.com/user-attachments/assets/8315835f-c1f5-480f-be3e-6aab5b028033)


- **ESP32 Camera devices:** 
Those came in sets, as seen in image in **[Hardware Chapter](#2-hardware)** with already prebuilt sets of Camera bus boards to be connected to Esp32-S boards and wired Antennas. So no additional wiring was required and only the casing to be built around it remained.

- **Hardware specifications and thoughts:** 
The hardware is relatively simple, requires 5V power, usually has USB-C/Micro USB ports. ESP32 boards have signal LEDs(Power on, Firmware flash/writing to memory), RGB LED(s) and Reset/Boot buttons. ESP32 Cameras(I have [OV2640](https://blog.arducam.com/ov2640/) in these sets) are fragile, small-frame and limited in there resolution/quality, but can be replaced with more serious counterparts.

**IMPORTANT NOTE!**
There is a really, _really_ imoprtant, critical note here!!! Do not buy cheap-ass ESP32 dev boards unless you want to go down a rabbit hole of guessing pinouts and missing documentation. If it costs under $4, something’s wrong — do make sure it’s an original board. Example - Espressif(I got it's knock off): almost $20 to my address [Link](https://aliexpress.ru/item/1005004494348761.html?sku_id=12000032953296653&spm=a2g2w.productlist.search_results.5.5863bc74XreuNA) Trust me, it’s worth the few extra bucks. Oterwise buying cheap components is a lottery. I ended up with 1 defective Esp32 S3 board, 1 fully defective esp32 Cam set and 2 broken DHT22 sensors. 

Other important thing to consider - those devices require GOOD Wi-Fi signal to operate reliably. Especially if we are talking about Cameras. For the CO2/Temperature/Humidity Sensors it's not that big of a deal, they dont have to send as much data. But, for ESP32 Cams you want your Wi-Fi to really reach them. Such cameras are rarely good for full on video security/survailance solutions but may good enogh to put your eyes on something critical in case other alarms/sensors go off - like electrical switchboxes, boilers, solar inverters/batteries/power walls or just common  kitchens with with fire hazards. 

My initial intent was to use them to monitor exactly such places, but it turned out Wi-Fi signal from basement with Boiler/Washing Machine/Pumps/Controllers was too weak. So if you have thick brick walls or other obstacles - be advised to investigate Wi-Fi signal strength prior to planning your video monitoring system!

To be fair, ESP32 Cams are successfully used as with Object detection/recognition systems like [Frigate](https://docs.frigate.video/integrations/home-assistant/) so feel free to experiment, but remember that price/quality/generation of components will have direct influence on results.


---

## 5. 📜 YAML Configuration (ESPHome)

ESPHome is a great place to start doing your DIY IOT(Internet Of Things) devices and finding custom approaches to unusual Smart Home challenges. As stated on their [web-site](https://esphome.io/):

_"ESPHome is an open-source firmware framework that simplifies the process of creating custom firmware for popular WiFi-enabled microcontrollers"_ 

ESPHome integrates perfectly with Home Assistant, it uses ESPHome Device Builder Add-on you can add from here:

[![Open this in Home Assistant](https://my.home-assistant.io/badges/supervisor_addon.svg)](https://my.home-assistant.io/redirect/supervisor_addon/?addon=5c53de3b_esphome&repository_url=https%3A%2F%2Fgithub.com%2Fesphome%2Fhome-assistant-addon)

The HA detects through auto-discovery if an ESPHome enabled device appears in your network or you can add it manually via Integration:

[![Open this in Home Assistant](https://my.home-assistant.io/badges/supervisor_addon.svg)](https://my.home-assistant.io/redirect/config_flow_start/?domain=esphome)

To flash ESPHome framework firmware on your device you can either do it from Builder Add-on or use [ESPHome Web](https://web.esphome.io/). Be sure to use USB cable with data transfer line and press (Boot) button if necessary(for most ESP32 boards) while connecting to USB port of your computer/HA server. Usually USB Device should be identified as USB JTAG something-something. Take a good look at [ESPHome documentation](https://esphome.io/guides/getting_started_hassio#) for HA, most of things are explained there. Also Google/ask nearest AI Chatbot for help - they work like a charm!

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


For **CO2/Temp/Humid(SCD41)** devices I have used following configuration:
```yaml
esphome:
  name: iot-esp32-bedroomnew-co2th
  friendly_name: Home CO₂/T/H Sensor – Bedroom
  name_add_mac_suffix: false

esp32:
  board: esp32-s3-devkitc-1
  framework:
    type: arduino  # Arduino framework for broad compatibility

# Enable logging for debugging (via serial)
logger:

# Home Assistant API for native integration
api:
  encryption:
    key: "REPLACE_WITH_API_ENCRYPTION_KEY"

# Enable OTA firmware updates
ota:
  - platform: esphome
    password: "REPLACE_WITH_OTA_PASSWORD"

# Static IP configuration for reliability
wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password
  power_save_mode: none
  domain: .your-domain.local
  manual_ip:
    static_ip: 192.168.1.176
    gateway: 192.168.1.1
    subnet: 255.255.255.0
    dns1: 192.168.1.1
    dns2: 8.8.8.8

# I²C communication bus for SCD41 sensor
i2c:
  sda: GPIO8
  scl: GPIO9
  scan: true
  id: bus_a

# SCD41 sensor – measures CO₂, temperature, humidity
sensor:
  - platform: scd4x
    id: scd41
    co2:
      name: "CO2 Bedroom"
      accuracy_decimals: 0
      unit_of_measurement: "ppm"
      id: scd41co2
    temperature:
      name: "Bedroom Temperature"
      accuracy_decimals: 1
      unit_of_measurement: "°C"
    humidity:
      name: "Bedroom Humidity"
      accuracy_decimals: 0
      unit_of_measurement: "%"
    update_interval: 15s

# Manually set a reference CO₂ value for calibration
number:
  - platform: template
    name: "CO₂ Calibration Reference"
    id: co2_calibration_value
    optimistic: true
    min_value: 400
    max_value: 2000
    step: 1
    initial_value: 400
    unit_of_measurement: "ppm"
    icon: "mdi:molecule-co2"

# Buttons to trigger forced calibration or factory reset
button:
  - platform: template
    name: "Calibrate CO₂ Sensor"
    icon: "mdi:calibration"
    on_press:
      then:
        - lambda: |-
            id(scd41).perform_forced_calibration(id(co2_calibration_value).state);
        - logger.log: 
            format: "Forced calibration with reference %d ppm"
            args: ["int(id(co2_calibration_value).state)"]

  - platform: template
    name: "CO₂ Sensor Factory Reset"
    icon: "mdi:restore"
    id: factory_reset_button
    on_press:
      then:
        - scd4x.factory_reset: scd41
        - logger.log: "SCD41 sensor factory reset initiated"

# Optional: Switch for enabling/disabling auto calibration
switch:
  - platform: template
    name: "CO₂ Auto Calibration"
    id: co2_auto_calibration
    optimistic: true
    restore_mode: RESTORE_DEFAULT_ON
    icon: "mdi:calibration"
    on_turn_on:
      - lambda: 'id(scd41).set_automatic_self_calibration(true);'
      - logger.log: "Enabled automatic self-calibration"
    on_turn_off:
      - lambda: 'id(scd41).set_automatic_self_calibration(false);'
      - logger.log: "Disabled automatic self-calibration"

```


For **ESP32 Cameras** things are a bit more complicated and should be tuned to your preference:
```yaml
esphome:
  name: "halaim-home-esp32-cam-entryway"
  friendly_name: Home ESP32 Cam – Entryway

esp32:
  board: esp32dev  # Generic ESP32 Dev Board
  framework:
    type: arduino

# Enable logging
logger:
  level: VERBOSE
  tx_buffer_size: 256

# Enable Home Assistant API + custom service for tuning camera settings on the fly
api:
  services:
    - service: camera_set_param
      variables:
        name: string
        value: int
      then:
        - lambda: |-
            bool state_return = false;
            if (("contrast" == name) && (value >= -2) && (value <= 2)) { id(espcam).set_contrast(value); state_return = true; }
            if (("brightness" == name) && (value >= -2) && (value <= 2)) { id(espcam).set_brightness(value); state_return = true; }
            if (("saturation" == name) && (value >= -2) && (value <= 2)) { id(espcam).set_saturation(value); state_return = true; }
            if (("special_effect" == name) && (value >= 0U) && (value <= 6U)) { id(espcam).set_special_effect((esphome::esp32_camera::ESP32SpecialEffect)value); state_return = true; }
            if (("aec_mode" == name) && (value >= 0U) && (value <= 1U)) { id(espcam).set_aec_mode((esphome::esp32_camera::ESP32GainControlMode)value); state_return = true; }
            if (("aec2" == name) && (value >= 0U) && (value <= 1U)) { id(espcam).set_aec2(value); state_return = true; }
            if (("ae_level" == name) && (value >= -2) && (value <= 2)) { id(espcam).set_ae_level(value); state_return = true; }
            if (("aec_value" == name) && (value >= 0U) && (value <= 1200U)) { id(espcam).set_aec_value(value); state_return = true; }
            if (("agc_mode" == name) && (value >= 0U) && (value <= 1U)) { id(espcam).set_agc_mode((esphome::esp32_camera::ESP32GainControlMode)value); state_return = true; }
            if (("agc_value" == name) && (value >= 0U) && (value <= 30U)) { id(espcam).set_agc_value(value); state_return = true; }
            if (("agc_gain_ceiling" == name) && (value >= 0U) && (value <= 6U)) { id(espcam).set_agc_gain_ceiling((esphome::esp32_camera::ESP32AgcGainCeiling)value); state_return = true; }
            if (("wb_mode" == name) && (value >= 0U) && (value <= 4U)) { id(espcam).set_wb_mode((esphome::esp32_camera::ESP32WhiteBalanceMode)value); state_return = true; }
            if (("test_pattern" == name) && (value >= 0U) && (value <= 1U)) { id(espcam).set_test_pattern(value); state_return = true; }

            if (true == state_return) {
              id(espcam).update_camera_parameters();
            } else {
              ESP_LOGW("esp32_camera_set_param", "Error in name or data range");
            }

# OTA updates
ota:
  - platform: esphome
    password: "REPLACE_WITH_PASSWORD"

# Network settings (static IP recommended for stability)
wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password
  power_save_mode: none
  domain: .your-domain.local
  manual_ip:
    static_ip: 192.168.1.212
    gateway: 192.168.1.1
    subnet: 255.255.255.0
    dns1: 192.168.1.1
    dns2: 8.8.8.8
  ap:
    ssid: "ESP32-CAM-Fallback"
    password: "StrongFallbackPass"

# Camera module configuration
esp32_camera:
  id: espcam
  name: "Entryway Camera"
  external_clock:
    pin: GPIO0
    frequency: 8MHz
  i2c_pins:
    sda: GPIO26
    scl: GPIO27
  data_pins: [GPIO5, GPIO18, GPIO19, GPIO21, GPIO36, GPIO39, GPIO34, GPIO35]
  vsync_pin: GPIO25
  href_pin: GPIO23
  pixel_clock_pin: GPIO22
  power_down_pin: GPIO32
  resolution: 1024x768  # SVGA
  jpeg_quality: 30       # 10–63 (lower is better quality)
  max_framerate: 25.0fps
  idle_framerate: 0.1fps
  frame_buffer_count: 2
  vertical_flip: false
  horizontal_mirror: false
  brightness: 2
  contrast: 1
  special_effect: none
  aec_mode: auto
  aec2: false
  ae_level: 0
  aec_value: 300
  agc_mode: auto
  agc_gain_ceiling: 4x
  agc_value: 0
  wb_mode: auto

# Lights (onboard white LED & red indicator)
output:
  - platform: ledc
    channel: 2
    pin: GPIO4
    id: espCamLED
  - platform: gpio
    pin:
      number: GPIO33
      inverted: True
    id: gpio_33

light:
  - platform: monochromatic
    output: espCamLED
    name: Entryway Cam Spotlight
  - platform: binary
    output: gpio_33
    name: Entryway Cam Status LED

# Restart switch + availability sensor
switch:
  - platform: restart
    name: Entryway Cam Restart

binary_sensor:
  - platform: status
    name: Entryway Cam Online

# Optional fallback access point
captive_portal:

# Built-in Web Server (stream & snapshot)
esp32_camera_web_server:
  - port: 8080
    mode: stream
  - port: 8081
    mode: snapshot
```
Key Parameters to Tune:

```text
jpeg_quality
```
Lower = better image quality (but larger payload).
Try: jpeg_quality: 10 for snapshots, 30 for balanced stream.

```text
_resolution_
```
Best real-world stability is around 1024x768. Going higher (e.g. UXGA) increases risk of ESP32 crashes unless you’re tuning buffers or using PSRAM-heavy variants.

```text
max_framerate
```
The ESP32 struggles above ~25fps. For low-light/stable monitoring, reduce this to 10.0 to decrease load.

```text
aec_value, ae_level
```
Manually tweak auto-exposure to prevent blown-out images or improve indoor low-light performance.

```text
agc_gain_ceiling
```
Controls max gain in darker scenes — raising it can improve night performance at the cost of noise.

```text
brightness / contrast / saturation
```
Adjust these per-scene with the exposed camera_set_param service for dynamic tuning from Home Assistant.

Other Advice:

> Enable vertical/horizontal flip if image is mounted upside-down or mirrored.

> Use esp32_camera_web_server for a fast local preview without involving HA.

> If images stutter or crash, lower resolution and/or framerate. Ensure static IP is used.


---

For network configuration I strongly recommend using Static IPv4s, Static DHCP entries(bind device MAC to local IP).
If you want a reliable, stress-proof system which will come back from power outages, networking issues/router faults - **set up manually as much as you consider healthy/sane** =) 
For me, with 100+ IoT devices of different sorts/brands/price ranges I had to learn it the hard way. 
As an example - I am happily using a separate DHCP Server running as [HA Add-on](https://github.com/f18m/ha-addon-dnsmasq-dhcp/tree/main) instead of shitty, trimmed-down version, found on most of consumer-level network equipment - my TP-Link is a good example of such a case. 
But, maybe you have a great network with Mikrotiks/Ubiquty/PFsense/etc. devices and sys-admin level skills, who knows, so.. you do you!


---


## 6. ⚖️ Calibration
When building DIY devices, raw data from hardware sensors often requires calibration to become reliable. Sensor readings may drift due to component tolerances, heat, or design flaws (such as proximity to heat sources or factory defects). Calibrating ensures the temperature (and other values) shown in Home Assistant reflect real-world conditions AND can be used in more complex Climate Automations without additional adjustments. For ESPHome configurations, we can add any offsets here, as an additional sensor platform in 
```yaml 
sensor:
```
part of config.


To take measurements it's best to use thermometers and hygrometers(for humidity). CO2 measurements without a sensor are extremely challenging and generally not feasible for accurate results - so compare against a better sensor if possible **\_0_/**. For this article I have used a good old lab mercury thermometer:

![Temp Sensor v2 Calibration Measurement 2](https://github.com/user-attachments/assets/da605666-da87-4097-bf1e-851bc1152dc9)


---

### 🔧 Common Calibration Methods

1. **Offset Correction (Linear)**
   - Add or subtract a fixed value to all readings.
   - Good when error is consistent across the range.
   - Example formula:
     ```text
     Calibrated = Raw - Offset
     ```
   - Example YAML:
     ```yaml
     sensor:
       - platform: template
         name: "Corrected Temperature"
         lambda: "return id(sensor_temp).state - 2.0;"
     ```

2. **Scaling Correction (Multiplicative)**
   - Multiply all readings by a factor (e.g., 0.97).
   - Useful when the sensor has linear but incorrect slope.
   - Example formula:
     ```text
     Calibrated = Raw × ScaleFactor
     ```
   - Example YAML:
     ```yaml
     sensor:
       - platform: template
         name: "Corrected Temperature"
         lambda: "return id(sensor_temp).state * 0.97;"
     ```

3. **Non-linear Correction (Custom Formula)**
   - Use a formula to describe how error changes depending on the reading.
   - Needed when error increases with temperature (in our example, due to heating from ESP32 chip/LEDs).
   - Formula and YAML example below

---

### 📈 Why We Used a Non-Linear Formula

Our sensors are mounted close to heat-emitting components (ESP32 chip, onboard LEDs), and even after updated casing design there are still deviasions. Problem is - relation is **not linear** and causes _higher error_ at _higher temperatures_.

Simple offsets (e.g., -2°C) can fix low temps but undercorrect for higher ones. A custom linear-plus-slope formula can give better correlation:

```text
Calibrated = Raw + slope × (Raw - reference_temp) - base_error
```
Where:
- `slope` adjusts correction rate as temp rises
- `reference_temp` is our calibration anchor (e.g., room temp)
- `base_error` is the estimated error at reference point

---

### 📊 Example Calibration Table

| Time  | Real Temp (Thermometer) | Raw Sensor | Difference |
|-------|--------------------------|------------|------------|
| 10:00 | 24.3 °C                  | 28.6 °C    | +4.3 °C    |
| 10:15 | 25.1 °C                  | 29.0 °C    | +3.9 °C    |
| 10:30 | 25.7 °C                  | 29.3 °C    | +3.6 °C    |
| 10:45 | 26.2 °C                  | 29.0 °C    | +2.8 °C    |
| 11:00 | 26.5 °C                  | 29.5 °C    | +3.0 °C    |
| 11:15 | 27.0 °C                  | 30.0 °C    | +3.0 °C    |
| 11:30 | 27.3 °C                  | 30.5 °C    | +3.2 °C    |
| 11:45 | 27.6 °C                  | 30.9 °C    | +3.3 °C    |
| 12:00 | 28.0 °C                  | 31.3 °C    | +3.3 °C    |
| 12:15 | 28.3 °C                  | 31.7 °C    | +3.4 °C    |

> 🔍 Note: The more readings you input, the more data points are available for curve fitting, resulting in a more precise calibration, even if it is non-linear relation. Think of it as this example illustrates:

![calibration_precision_curve](https://github.com/user-attachments/assets/8e7c2ca5-2a68-4e35-8385-88897088ddee)


---

### 🧮 Final Calibration Formula (YAML)

Based on the updated calibration table, we recalculate our formula with improved values:

```text
Calibrated = Raw + (-0.31 × (Raw - 24.0)) - 2.3
```

Updated YAML:

```yaml
sensor:
  - platform: template
    name: "BedroomOld Temperature Calibrated"
    unit_of_measurement: "°C"
    accuracy_decimals: 1
    lambda: |-
      float slope = -0.31;
      float reference_temp = 24.0;
      float base_error = 2.3;
      return id(scd41_temperature).state + (slope * (id(scd41_temperature).state - reference_temp)) - base_error;
    update_interval: 15s
```

---

### ✅ Results & Final Thoughts

- **Before Calibration:** ~+5 to +8°C error due to heat buildup
- **After Calibration:** Reduced to ~+0.6 to +1.2°C error
- **How to improve:** Possibly refine further using [polynomial regression](https://en.wikipedia.org/wiki/Polynomial_regression) or add ambient board temperature sensor directly to the chip. But this is overcomplicating simple device beyond the point of reasonable. Unless your specific situation requires it.

Calibration is always an iterative process. While this current formula may still be adjusted in the future, it already yields realistically usable values in Home Assistant dashboards and automations. At the end of the day, climate or air quality automations are about **subjective comfort** — measured against available data and, more importantly, **how that data changes over time**. Near-perfect precision is great, but practical **consistency** is what actually makes a smart home feel smart over time.


---

## 7. 🏠 Integration with Home Assistant
- Integrated via ESPHome native API
- Entity names standardized for clarity (e.g., `sensor.living_room_co2`)
- Used in:
  - Dashboard badges & cards
  - Alarm triggers
  - Automation for ventilation/humidification

---

## 8. 🖥️ UI & Dashboards
- Designed dashboards for **tablets** and **mobile phones** (portrait + landscape)
- Devices added to room views, gauge cards, graphs
- Bonus: CO₂ LED alert on sensor body for quick glance
- Linked dashboard repo: [Home Assistant Dashboards](https://github.com/AlexeiakaTechnik/Practial-and-stylish-Home-Assistant-Dashboards-for-Tablets-and-Mobile-Phones)

---

## 9. 🌈 Bonus – Visual CO₂ Indicator with RGB LED

To improve usability and glance-based monitoring, I used the onboard WS2812 RGB LED available on my ESP32-S3 boards to display a visual indicator of current CO₂ levels.

The LED changes color depending on air quality:
- 🟢 Green — Good (CO₂ < 1000 ppm)
- 🟡 Yellow — Moderate (1000–1500 ppm)
- 🔴 Red — Poor (CO₂ > 1500 ppm)

### 🔌 Important Notes:
- You need to **know the exact GPIO pin** your RGB LED is connected to (usually found in board documentation or by experimenting).
- The LED should be addressable (WS2812 or similar), and configured via `neopixelbus` or `fastled_clockless` in ESPHome.

### 🧠 YAML Example:

```yaml
# Define a single WS2812 RGB LED connected to GPIO48
light:
  - platform: neopixelbus
    pin: GPIO48
    variant: WS2812         # Type of RGB LED used
    num_leds: 1             # Only one LED in use
    type: GRB               # LED color ordering
    name: "CO2/T/H Sensor Bedroom RGB LED"
    id: esp32_led
    default_transition_length: 1s  # Smooth transition when turning on/off

# Define global variables to store current RGB values
globals:
  - id: led_red
    type: int
    restore_value: no
    initial_value: '0'
  - id: led_green
    type: int
    restore_value: no
    initial_value: '255'   # Start with green (good air quality)
  - id: led_blue
    type: int
    restore_value: no
    initial_value: '0'

# Script to flash the LED with a color based on CO2 level
script:
  - id: flash_led
    mode: restart  # Cancel and restart if already running
    then:
      - lambda: |-
          float co2_value = id(scd41co2).state;

          // Default to green = good air quality
          id(led_red) = 0;
          id(led_green) = 255;
          id(led_blue) = 0;

          // Yellow warning: moderate CO2
          if (co2_value > 1000) {
            id(led_red) = 255;
            id(led_green) = 255;
            id(led_blue) = 0;
          }

          // Red warning: high CO2 level
          if (co2_value > 1500) {
            id(led_red) = 255;
            id(led_green) = 0;
            id(led_blue) = 0;
          }

      - repeat:
          count: 5  # Flash LED 5 times
          then:
            - light.turn_on:
                id: esp32_led
                red: !lambda "return id(led_red) / 255.0;"    # Normalize to 0.0–1.0
                green: !lambda "return id(led_green) / 255.0;"
                blue: !lambda "return id(led_blue) / 255.0;"
            - delay: 1.5s
            - light.turn_off: esp32_led
            - delay: 1.5s

# Automatically check CO2 level and trigger LED every 60 seconds
interval:
  - interval: 60s
    then:
      - script.execute: flash_led
```
And here is a video of how it works/looks like:

[![Visual LED CO2 Level Indication](https://img.youtube.com/vi/ZwWRNItUULs/0.jpg)](https://www.youtube.com/watch?v=ZwWRNItUULs)


You can also tie the LED to motion, alarm states, or other values — just update the script logic.

---

## 10. 💬 Final Thoughts

This was an intense, prolonged and sometimes frustrating project. But in measure of experience rewards it is priceless to me. I built something real, tangible, and useful for my smart home. Came away with the skills to replicate and expand it, with curiosity of more complicated solutions and with dread of what actual R&D engineers have to go through. Nah, just kidding, those guys and gals have an awesome job - tinker with stuff and get paid for it.

Regarding DIY projects like this - well, it's a hobby. If you want to compete with commercial devices - you definately have to find a niche, maybe some open source project, promotion for specific crowd, like a lot of bloggers/youtubers/communities end up with their own designs/brands sold to fellow enthusiasts. But the mass market is powered by whole teams and departments who design IoT devices for a living ... 

So let's **compare prices**, just the parts for DIY vs ready-available sensors. No labor, no hours put into learning/research, no fails, no faulty parts and no configuration/calibration hassle. 

For me, Temperature & Humidity Detector was:
ESP32 Board: $
DHT22 Sensor: $
Power supply/adapter: $
Cable: $
3D Printing parts for a single device: $

Commercial Detector I bought and use at home:
Price(with delivery): $

All the while, we presume that commercial detector has low error margin, is powered by a small CR2032 battery, is smaller, more stable and reliable, uses Zigbee wireless protocol instead of Wi-Fi(lower power consumption, less networking configuration), is configured to be power efficient(wake up, trace if there was a change, send readings, go to sleep by default). And it is slick, complete and polished.

But! The DIY ESP32 based platform can be transformed, expanded with additional hardware, additional sensors to additional pins, used for robots, lighting, BLE beacon tracking, physical automations - maybe several of those at the same time. It can be re-configured, updated, fully controlled. It does not require cloud, will not send any data anywhere you don't want it to. And it can be a great start to learn other things if you are into it.

So, my final verdict is: Be sure to ask the right question - What are **you** looking for?

And my hope is that this inspires other makers, engineers from other areas, tinkerers, and Smart Home beginners to realize they don’t need to buy into expensive ecosystems or pricy DIY sets to start experimenting. You can do so much more with some effort, creativity, imagination and a few sensors. Please reach out if you want to collaborate, have questions or just want to share your experience!

---

## 11. 📚 Related Articles
- [HA UI/Dashboards](https://github.com/AlexeiakaTechnik/Practial-and-stylish-Home-Assistant-Dashboards-for-Tablets-and-Mobile-Phones)
- [My Repositories/Articles](https://github.com/AlexeiakaTechnik/Alexei-Halaim-Smart-Home-Portfolio_Articles-list)
