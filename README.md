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
- [X] PCB rev.A hardware validated
- [X] Initial bring-up with ArduPilot firmware
- [X] Lua scripting verified
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

## Flashing
With a fresh board we must flash the ardupilot bootloader. This requires us to put the mcu in DFU mode, which is done by holding down the boot button while powering on the board.

### Ardupilot + bootloader
1. Hold down boot button while powering on the board. If you're on linux you can use `dmesg -w` to monitor usb acitivty and you should get something like `Product: DFU in FS Mode` show up.
2. Open STM32CubeProgrammer and connect with USB
3. Open the file in `binaries/arducopter_with_bl.hex` and press flash
4. Powercycle the board and you should see `bjorke-BL` registers itself as USB device at first, then once it leaves bootloader you should get `bjorke` as USB device, and a serial port, eg `/dev/ttyACM0`

### Ardupilot application only
1. Using the `uploader.py` in AP repo
    ```
    python3 Tools/scripts/uploader.py build/bjorke/bin/arducopter.apj
    ```
2. Or, after built in repo: 
    ```
    ./waf copter --upload
    ```

### Ardupilot bootloader only
1. Put into DFU (same as above)
2. Flash bootloader using either STM32CubeProgrammer, or `dfu-util` with:
    ```
    dfu-util -a 0 --dfuse-address 0x08000000 -D binaries/AP_Bootloader.bin -R
    ```

### Building the code
Enter the ardupilot repository and run:

#### Bootloader
Either using:
```
./Tools/scripts/build_bootloaders.py bjorke
```
Creates binaries in `Tools/bootloaders/`:
- `Tools/bootloaders/bjorke_bl.bin`
- `Tools/bootloaders/bjorke_bl.hex`

Or, using:
```
./waf configure --board bjorke --bootloader
./waf clean
./waf bootloader
```

Bootloader binaries should be built to `build/bjorke/bin`
- AP_Bootloader.apj
- AP_Bootloader.bin
- AP_Bootloader.hex

#### Application
For the application build we first must have built bootloader with `./Tools/scripts/build_bootloaders.py`.
This is because AP tooling seems to expect a bootloader binary in `Tools/bootloaders/`.

```
./waf configure --board bjorke
./waf copter
```
