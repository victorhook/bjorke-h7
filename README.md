# 🛩️ Bjorke H7 Flight Controller

Bjorke H7 is a fully open source high-performance, ArduPilot-compatible flight controller built around the powerful STM32H743VIT6 MCU. Designed for flexibility and reliability, it supports a wide range of applications—from autonomous drones to experimental robotics.

---

## 🔧 Key Features

### ⚙️ Processing Power
- **MCU**: STM32H743VIT6 (480 MHz, 2MB Flash, 1MB RAM)

### 🧭 Sensors
- **IMU**: ICM-42688-P – ultra-low noise 6-axis motion tracking
- **Barometer**: BMP388 – high-accuracy altimeter for reliable altitude estimation

### 🔄 Interfaces & I/O
- **8x Motor Outputs** via 2x ESC 8-pin JST connectors
- **8x UARTs** for telemetry, GPS, companion computers, etc.
- **1x I²C** for external sensors or peripherals
- **3x Servo Outputs** + **1x dedicated GPIO**
- **1x RGB Status LED**
- **2x extra ADC Input Pins** for external sensors
- **1x CAN** (with onboard TJA1051TK/3 transceiver) – plug-and-play UAVCAN support

### 💾 Storage & Logging
- **MicroSD card slot** for robust onboard logging

### 🔌 Power Architecture
- **5V @ 3A** DC-DC
- **3.3V @ 3A** DC-DC

---

## ⚡ Designed for ArduPilot
Bjorke H7 runs **ArduPilot firmware** with support for:
- Real-time telemetry
- In-flight parameter updates
- MAVLink compatibility
- Full hardware-in-the-loop (HITL) testing
- CAN-based peripherals (UAVCAN GPS, ESCs, etc.)

---

## 🚧 Status
- [X] PCB rev.A designed and ordered
- [X] hwdef.dat
- [ ] PCB rev.A hardware validated
- [ ] Initial bring-up with ArduPilot firmware
- [ ] Lua scripting verified
- [ ] First takeoff achieved
- [ ] 1 hour flight time achieved
- [ ] 5 hours flight time achieved
- [ ] 10 hours flight time achieved
- [ ] 25 hours flight time achieved
- [ ] 50 hours flight time achieved
- [ ] 100 hours flight time achieved

---

## 🧪 Ideal for:
- Custom drones (quads, hexas, octos)
- Research platforms
- Robotics
- Developers who need **max control and visibility**


