# ESP32C3 Smart Board

**Product Name:** ESP32C3 Smart Board  
**Board Revision:** 1.3  
**Updated:** 26.12.2025  
**Author:** Marko Petrov (petrovgp)  

---

## 1. General Description

The ESP32C3 Smart board is a compact, battery-powered ESP32-based development board designed in **KiCad 9**, integrating power management, motion sensing, and display support in a small form factor. Ideal for low-power IoT or wearable applications.

---

## 2. Features

- ESP32 C3 MCU
    - ESP32C3FH4, RISC-V single-core 32-bit processor, up to 160 MHz
    - 4MB internal flash
    - 400KB SRAM
    - Wi-Fi 2.4 GHz IEEE 802.11 b/g/n
    - Bluetooth 5 (LE)
- ME6211A LDO regulator
    - 3.3V output voltage
    - 500mA max output current
    - 100mV @ 100mA dropout voltage
- Li-ion charging and protection ICs
    - TP4056 charging IC configured at 250mA
    - DW01A + FS8205A protection ICs
    - Power sharing circuit for use while charging
- MPU6050 accelerometer
    - Supports interrupt mode with INT pin
- GC9A01 display
    - 240x240 TFT color display
    - Supports up to 40MHz (40Mbps) on hardware SPI
- USB Type C connector
    - Power and programming interface for ESP32C3

---

## 3. Functional Block Diagram

```mermaid
flowchart LR
    %% =====================
    %% Power Path
    %% =====================
    subgraph Power["Power Path"]
        A[USB Type-C] -->|VBUS| B{Power Sharing Circuit}
        A --> C[TP4056 Li-Ion Charger]
        C -->|BAT| D[Li-Ion Battery]
        D -->|VBAT| B
        B -->|VCC| E[ME6211A LDO]
    end

    %% =====================
    %% Main System
    %% =====================
    subgraph System["System & Peripherals"]
        E -->|3V3| MCU[ESP32C3]
        E -->|3V3| DISP[GC9A01 Display]
        E -->|3V3| IMU[MPU6050 IMU]
    end

    %% =====================
    %% Data Interfaces
    %% =====================
    MCU <-->|I2C| IMU
    MCU <-->|SPI| DISP
```

---

## 4. Absolute Maximum Ratings

### Voltage ratings

| Parameter                      | Min | Typ | Max | Unit |
|--------------------------------|-----|-----|-----|------|
| USB Type C voltage (VBUS)      | 4.0 | 5.0 | 6.5 |   V  |
| Battery voltage (VBAT)         | -0.3| 3.6 | 4.2 |   V  |
| High-level input voltage (VIH) | 2.5 |  -  | 3.6 |   V  |
| Low-level input voltage (VIL)  | -0.3|  -  | 0.8 |   V  |
| High-level output voltage (VOH)| 2.6 |  -  |  -  |   V  |
| Low-level output voltage (VOL) |  -  |  -  | 0.33|   V  |
| Ambient temperature            | -40 | 25  | 125 |  °C  |


### Current ratings

| Parameter                        | Min | Typ | Max | Unit |
|----------------------------------|-----|-----|-----|------|
| Input current (IBUS), w/ battery | 250 | 350 | 630 |  mA  |
| Input current (IBUS), no battery | 0.02| 100 | 380 |  mA  |
| Battery charing current          |  -  | 250 |  -  |  mA  |

> Recommended operating conditions are the typical values

---

## 5. Pin configurations

```mermaid
graph LR
    %% Nodes
    MCU((Microcontroller))
    DISP["GC9A01 Display"]
    IMU["MPU6050 IMU"]
    UART["Exposed UART port"]
    USBC["USB Type C port"]

    %% Pins (subgraph style)
    subgraph MCU_PINS["MCU Pins"]
        MCU_GPIO0["GPIO0 / I2C_SDA"]
        MCU_GPIO1["GPIO1 / I2C_SCL"]
        MCU_GPIO4["GPIO4 / SPI_CLK"]
        MCU_GPIO6["GPIO6 / SPI_DATA"]
        MCU_GPIO7["GPIO7 / SPI_CS"]
        MCU_GPIO8["GPIO8 / RESET"]
        MCU_GPIO2["GPIO2 / BL"]
        MCU_GPIO3["GPIO3 / DC"]
        MCU_GPIO10["GPIO10 / MPU_INT"]
        MCU_GPIO18["GPIO18 / USB_D-"]
        MCU_GPIO19["GPIO19 / USB_D+"]
        MCU_GPIO20["GPIO20 / U0RX"]
        MCU_GPIO21["GPIO21 / U0TX"]
    end

    %% Connections
    MCU_GPIO0 --> |I2C_SDA| IMU
    MCU_GPIO1 --> |I2C_SCL| IMU
    MCU_GPIO10 --> |MPU_INT| IMU

    MCU_GPIO4 --> |SPI_CLK| DISP
    MCU_GPIO6 --> |SPI_MOSI| DISP
    MCU_GPIO7 --> |SPI_CS| DISP
    MCU_GPIO8 --> |RESET| DISP
    MCU_GPIO2 --> |PWM BL| DISP
    MCU_GPIO3 --> |DC| DISP

    MCU_GPIO18 --> |USB_D-| USBC
    MCU_GPIO19 --> |USB_D+| USBC

    MCU_GPIO20 --> |U0RX| UART
    MCU_GPIO21 --> |U0TX| UART

    %% Style
    classDef mcuPins fill:#FF0000,stroke:#333,stroke-width:2px;
    class MCU_GPIO0,MCU_GPIO1,MCU_XTALN,MCU_XTALP,MCU_GPIO4,MCU_GPIO6,MCU_GPIO7,MCU_GPIO8,MCU_GPIO2,MCU_GPIO3,MCU_GPIO10,MCU_GPIO18,MCU_GPIO19,MCU_GPIO20,MCU_GPIO21 mcuPins;
```
---