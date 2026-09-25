# Range Master Pro Shooting Timer & Light System

**Version**: 2.0 (Dual-Mode Wired UART + Wireless ESP-NOW)  
**Ref Document**: QUA/INC/2026/018-R10  

---

## 🚀 Quick Start Instructions for Your Friend

### 1. Test the Web Simulator Immediately (No Installation Needed!)
1. Open the `web_simulator` folder.
2. Double-click **`index.html`** to launch the interactive simulator in Google Chrome, Microsoft Edge, or Firefox.
3. Use the **Rotary Knob** / Dropdowns to pick a Series (1-8 ISSF or 9. Custom Series) and Load Time (15s, 30s, or 60s).
4. Click **PRESS START**.
5. When the Green Light turns ON, press the **SPACEBAR** (or click **💥 BANG!**) to simulate gunshots. Up to 5 shots will be captured with **Timer 1 (Total Time)**, **Timer 2 (Split Time)**, and **Late Shot Delay Detection (>0.2s)**!

---

## 📂 Project Directory Structure

```text
shooting_range_timer/
├── README.md                              <- Project overview & quick guide (this file)
├── web_simulator/
│   └── index.html                         <- Standalone web simulator (open in any browser)
├── master_firmware/
│   └── master_control_unit.ino            <- Master Transmitter Firmware (ESP32-WROOM-32)
├── slave_firmware/
│   └── slave_light_panel.ino              <- Slave Target Light Panel Firmware (ESP32-C3)
├── esp32_c3_super_mini_receiver/
│   └── esp32_c3_super_mini_receiver.ino  <- Alternative ESP32-C3 Super Mini Receiver
├── issf_pistol_timer_working_process.md   <- Full Flowchart & Timing Specifications
├── shooting_range_build_guide.md          <- Hardware Pinout & Wiring Diagram
└── shooting_range_sow_summary.md          <- SOW Technical Summary & BOM Breakdown
```

---

## 🛠️ Hardware Requirements & Wiring

### 1. Master Control Unit (ESP32-WROOM-32)
- **Display**: ST7789 / ILI9341 2.8" SPI TFT Display
- **Audio**: DFPlayer Mini MP3 Module + 3W Speaker
- **Sensor**: MAX4466 Acoustic Microphone Module (`GPIO 35`)
- **Controls**: Rotary Encoder (`GPIO 25`, `26`, `27`) + Illuminated Push Buttons (`GPIO 32`, `33`)
- **Cable Output**: Wired 4-core UART signal on `GPIO 15`

### 2. Slave Target Light Panel (ESP32-C3)
- **Matrix**: 8x8 WS2812 RGB LED Matrix (`GPIO 8`)
- **Signal Input**: Dual Wired Cable RX (`GPIO 20`) + ESP-NOW 2.4GHz Direct Wireless

---

## 🎵 DFPlayer Mini Audio Track List

Place the following `.mp3` files in an `mp3` folder on a MicroSD card inserted into the DFPlayer Mini:

- `0001.mp3` — *"4 Minutes Series"*
- `0002.mp3` — *"5 by 3 Seconds Series"*
- `0003.mp3` — *"20 Seconds Series"*
- `0004.mp3` — *"10 Seconds Series"*
- `0005.mp3` — *"8 Seconds Series"*
- `0006.mp3` — *"6 Seconds Series"*
- `0007.mp3` — *"4 Seconds Series"*
- `0008.mp3` — *"150 Seconds Series"*
- `0009.mp3` — *"Custom Series"*
- `0010.mp3` — *"LOAD"*
- `0011.mp3` — *"ATTENTION"*
- `0012.mp3` — *"UNLOAD"*

---

## 🚥 Color Process Rules

1. **LOAD Phase (15s / 30s / 60s)**: Target LED Panel is **OFF / DARK** (`RGB: 0, 0, 0`).
2. **ATTENTION Phase (7s)**: Target LED Panel illuminates **SOLID RED** (`RGB: 255, 0, 0`) for **7 seconds**.
3. **SHOOTING Phase**: Target LED Panel illuminates **SOLID GREEN** (`RGB: 0, 255, 0`) for the event duration.
4. **STOP Phase (7s)**: Target LED Panel illuminates **SOLID RED** (`RGB: 255, 0, 0`) for **7 seconds**.
5. **UNLOAD Phase**: Target LED Panel returns to **OFF / DARK** (`RGB: 0, 0, 0`).
