# Range Master Pro Timer — Acoustic Gunshot Sensor & Split Time Guide

**Device Feature:** Acoustic Gunshot Sensor & Split Time Recorder  
**Sensor Module:** MAX4466 Electret Microphone Module (with Adjustable Gain Trimpot) or MAX9814 AGC  
**Pin Connection:** `OUT` connected to ESP32-WROOM `GPIO 35` (ADC Pin)

---

## 🎤 1. How Acoustic Gunshot Detection Works

```mermaid
flowchart LR
    GUNSHOT["💥 Gunshot Acoustic Impulse<br/>(Loud High-Decibel Spike)"] --> MIC["MAX4466 Microphone Sensor"]
    MIC -- "Analog Voltage Output (OUT)" --> ADC["ESP32 GPIO 35 (ADC Pin)"]
    ADC --> PEAK["Peak Threshold Check<br/>(micValue > 2600)"]
    PEAK --> TIMESTAMP["Record Timestamp & Split Time<br/>(Shot 1..5, AVG, TOTAL)"]
    TIMESTAMP --> TFT["Render Green Bar Graph on 2.8\" TFT Screen"]
```

---

## 🔌 2. MAX4466 Microphone Wiring

| Sensor Pin | ESP32-WROOM-32 Connection | Function |
| :--- | :--- | :--- |
| **VCC** | 3.3V Pin | Power Supply (3.3V Clean Rail) |
| **GND** | GND Pin | Ground |
| **OUT** | **GPIO 35** (Analog Input ADC1_CH7) | High-speed acoustic peak signal |

> 💡 **Calibration Tip:** Turn the small gold trimpot on the back of the MAX4466 module using a screwdriver to set sensitivity. Adjust so normal talking does not trigger a shot, but a loud gunshot or handclap instantly registers as a shot!

---

## 📁 3. Code & Simulator File Links

- 🌐 **[index.html Interactive Gunshot Simulator](file:///C:/Users/DELL/.gemini/antigravity/scratch/shooting_range_timer/web_simulator/index.html):** Click **`💥 BANG! (FIRE SHOT)`** or press **`SPACEBAR`** during Green Light to record live split times!
- ⚡ **[master_control_unit.ino Firmware](file:///C:/Users/DELL/.gemini/antigravity/scratch/shooting_range_timer/master_firmware/master_control_unit.ino):** Full ESP32 firmware with MAX4466 acoustic gunshot sensing on `GPIO 35`.
- 🛠️ **[shooting_range_build_guide.md](file:///C:/Users/DELL/.gemini/antigravity/brain/de2fd286-f8ac-47ea-a8ea-390586c988ad/shooting_range_build_guide.md):** Complete hardware build & assembly guide.
