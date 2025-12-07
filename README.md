# Arduino EEPROM Programmer (28C16)

![Arduino](https://img.shields.io/badge/Arduino-00979D?logo=arduino&logoColor=white)
![KiCad](https://img.shields.io/badge/KiCad-blue?logo=kicad&logoColor=white)
![License](https://img.shields.io/badge/license-CC0_1.0-lightgrey)

A custom PCB shield and Arduino firmware designed to program **28C16 Parallel EEPROMs**.

This tool is essential for projects like the **Ben Eater 8-bit computer**, allowing you to burn microcode or 7-segment display logic into non-volatile memory without manually toggling dip switches.

## 🔌 Hardware Design (KiCad)
The `gerbers/` and root directory contain the full design files for a custom PCB that fits on top of an Arduino (or connects via headers).

* **Chip Support:** 28C16 (2K x 8-bit Parallel EEPROM).
* **Design Tool:** KiCad (Schematic & PCB files included).
* **Status:** Production-ready Gerber files are available in the `gerbers` folder.

### 📸 PCB Preview
<p align="center">
  <img src="https://github.com/user-attachments/assets/5b131cb6-19a5-4499-ba8f-2b032ae5f308" alt="PCB 3D Render" width="600">
</p>

## 💻 Firmware (Arduino)
The C++ code in `arduino_programmer/` handles the write cycle timing and address management.

### Key Features
* **Write Cycle Control:** Manages the Write Enable (WE) and Chip Enable (CE) pulses required by the 28C16 datasheet.
* **7-Segment Decoding:** By default, the code includes a lookup table to program the EEPROM with hexadecimal digits (0-9) for a common-cathode 7-segment display.
* **Customizable:** You can modify the `data` array to burn any microcode instruction set.

## 🚀 Getting Started

### 1. Fabrication / Wiring
You can either:
* **Order the PCB:** upload the zip gerber files to a PCB manufacturer (JLCPCB, PCBWay, etc.).
* **Breadboard it:** Follow the pinout defined in the `arduino_programmer.ino` file to wire the EEPROM directly to the Arduino digital pins.

### 2. Flashing
1.  Open `arduino_programmer/arduino_programmer.ino` in the Arduino IDE.
2.  Connect your Arduino.
3.  **Verify the pin definitions** at the top of the file match your wiring.
4.  Upload the sketch.
5.  Open the **Serial Monitor** (57600 baud) to see the programming status.

## ⚠️ Important Notes

* **Timing:** The 28C16 requires a specific write pulse width (usually < 1ms). The code handles this, but check your specific datasheet if using a different variant (e.g., 28C64).

