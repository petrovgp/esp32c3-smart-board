# ESP32-C3 Smart Board

A compact, battery-powered ESP32-C3 development board designed in **KiCad 9**, integrating power management, motion sensing, and display support in a small form factor. Ideal for low-power IoT or wearable applications.

## 🏢 Sponsor of today's project - PCBWay!

A huge thank you to PCBWay for sponsoring this project!

PCBWay provided high-quality PCB fabrication and assembly support, helping bring the hardware from prototype to reality. Their fast turnaround times, excellent communication, and reliable manufacturing made a big difference in the development process.

If you're looking for PCB manufacturing, assembly, CNC, or 3D-printing services, check out PCBWay **[here!](https://www.pcbway.com)**

Production files for this project were created using PCBWay KiCAD plugin and they can be used in PCBWay PCB and PCBA services right away!

Thanks again to PCBWay for supporting open-source hardware projects!

## 📸 Board design
![alt text](https://github.com/petrovgp/esp32c3-smart-board/blob/main/images/esp32c3-smart-board-front.jpg?raw=true)
![alt text](https://github.com/petrovgp/esp32c3-smart-board/blob/main/images/esp32c3-smart-board-back.jpg?raw=true)

---

## 🧠 Features

### ⚡ Core
- **ESP32-C3** RISC-V microcontroller with Wi-Fi and BLE 5.0
- Compact **42 × 45 mm** PCB designed in KiCad 9
- Integrated **Inverted-F antenna** for stable wireless performance

### 🔋 Power System
- Operable from **Li-Ion / Li-Po battery** and **USB Type C**
- On-board **TP4056** linear charging IC
  - 250mA charging current configuration
- **DW01A + FS8205A** dual MOSFET battery protection circuit
- Power-sharing design — board can operate **while charging**
- **ME6211C** LDO regulator:
  - 500 mA max output current
  - 100 mV dropout at 100 mA

### 🧭 Sensors
- **MPU6050** 6-axis accelerometer and gyroscope  
  - Interrupt pin connected to ESP32-C3 for motion wake-up or gesture detection

### 🖥️ Display
- **GC9A01** round TFT display connector
  - 12-pin FPC interface for bare display module

### 🔌 Connectivity
- **USB Type-C** connector for power and programming
- Exposed UART pins for debugging

## 🧩 Production files
All design files were created in **KiCad 9** and production files have been exported with **PCBWay plugin** (available **[here](https://github.com/pcbway/PCBWay-Plug-in-for-Kicad.git)**):
- `schematics/` – full circuit schematics
- `kicad/` – KiCAD 9 project files
- `kicad/production/` – ready-to-manufacture files (GERBERs + BOM)

Adjustment of production files might be needed. Please check carefully before placing any manufacturing orders.

## 🧾 Revisions

| Revision | Manufactured | Notes | Available |
|-----------|------|-------|-----------|
| **v1.0** | Nov 2025 | Improper GC9A01 footprint (wrong pitch), improper PMOS power sharing footprint (SOT23-5 instead of SOT23-3), everything else verified as OK  | Not available on Github
| **v1.1** | _Not manufactured_ | Updated GC9A01 footprint pitch, updated PMOS power sharing footprint, layout and silkscreen changes | Tagged v1.1 on Github
| **v1.2** | Dec 2025 | Layout and silkscreen changes | Tagged v1.2 on Github
| **v1.3** | _Not manufactured_ | Footprint changes, battery section layout changes, rounded antenna trace, bottom layer 3.3V plane addition, layout and silkscreen changes| Tagged v1.3 on Github
