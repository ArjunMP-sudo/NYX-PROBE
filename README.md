<div align="center">

<!-- HEADER -->
<img src="https://capsule-render.vercel.app/api?type=waving&color=0:00ffff,50:1a0033,100:ff006e&height=140&section=header&text=NYX%20PROBE&fontSize=50&fontColor=00ffff&fontAlignY=60&animation=fadeIn" width="100%"/>

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=18&duration=3000&pause=1500&color=00FFFF&center=true&vCenter=true&width=700&lines=ESP32+Multi-Function+Pentesting+Platform;WiFi+%7C+BLE+%7C+Network+%7C+GPS+%7C+HID+Attacks;Interactive+OLED+Interface;Built+for+Field+Security+Testing" alt="NYX Description" />

<br/>

[![GitHub](https://img.shields.io/badge/GitHub-ArjunMP--sudo-000000?style=flat-square&logo=github&logoColor=00ffff)](https://github.com/ArjunMP-sudo)
[![Status](https://img.shields.io/badge/Status-ACTIVE%20DEVELOPMENT-red?style=flat-square)](https://github.com/ArjunMP-sudo/NYX-Probe-Firmware)
[![License](https://img.shields.io/badge/License-MIT-9B00FF?style=flat-square)](LICENSE)
[![ESP32](https://img.shields.io/badge/Platform-ESP32-000000?style=flat-square&logo=espressif&logoColor=00ffff)]()
[![C++](https://img.shields.io/badge/Language-C%2B%2B-000000?style=flat-square&logo=cplusplus&logoColor=9B00FF)]()

</div>

---

## 〈 PROJECT OVERVIEW 〉

**NYX Probe** is a comprehensive ESP32-based hardware pentesting platform for authorized security testing, research, and education. It combines WiFi analysis, Bluetooth/BLE assessment, network scanning, GPS functionality, and HID attacks into a single portable device with an intuitive OLED interface.

```
╔═══════════════════════════════════════════════════════════╗
║         NYX PROBE - TACTICAL SECURITY PLATFORM            ║
╠═══════════════════════════════════════════════════════════╣
║  • WiFi Security Analysis & Testing                       ║
║  • Bluetooth/BLE Reconnaissance & Attacks                 ║
║  • Network Service Discovery & Port Scanning              ║
║  • GPS Location Tracking & Wardriving                     ║
║  • BLE Human Interface Device (HID) Attacks               ║
║  • Real-time Signal Monitoring & Analysis                 ║
║  • Intuitive Interactive OLED Menu System                 ║
╚═══════════════════════════════════════════════════════════╝
```

---

## 〈 HARDWARE REQUIREMENTS 〉

| Component | Specification | Notes |
|-----------|---------------|-------|
| **Microcontroller** | ESP32 (WROOM-32 or WROVER) | Dual-core, WiFi + BLE |
| **Display** | 128x64 OLED (SSD1306) | I2C connection |
| **GPS Module** | GY-NEO6MV2 or NEO-8M | Optional, UART/I2C |
| **Power** | 3.7V Li-ion Battery | 1000mAh+ recommended |
| **Buttons** | Momentary push buttons (3-4) | Navigation and action |
| **Enclosure** | 3D-printed or project box | Custom build |

### Default GPIO Pinout
```cpp
// OLED Display (I2C)
SDA  → GPIO 21
SCL  → GPIO 22
VCC  → 3.3V
GND  → GND

// Navigation Buttons
UP    → GPIO 25
DOWN  → GPIO 26
SEL   → GPIO 27
BACK  → GPIO 14

// GPS (Optional)
RX → GPIO 16
TX → GPIO 17

// Status LED (Optional)
LED → GPIO 2
```

Edit `config.h` to customize pins for your setup.

---

## 〈 FLASHING FIRMWARE 〉

### Method 1: PlatformIO (Recommended)

**Prerequisites:**
- Install [Visual Studio Code](https://code.visualstudio.com/)
- Install PlatformIO extension (VSCode → Extensions → search "PlatformIO")
- USB cable to connect ESP32

**Steps:**
```bash
# 1. Clone repository
git clone https://github.com/ArjunMP-sudo/NYX-Probe-Firmware.git
cd NYX-Probe-Firmware

# 2. Install dependencies
platformio lib install

# 3. Connect ESP32 via USB

# 4. Select correct COM port
# PlatformIO → Project Tasks → ESP32 → General → Select Serial Port

# 5. Build and upload firmware
platformio run --target upload

# 6. Monitor serial output
platformio device monitor
```

### Method 2: Arduino IDE

**Prerequisites:**
- Download [Arduino IDE](https://www.arduino.cc/en/software) (v1.8.19+)
- Install ESP32 board support:
  - File → Preferences
  - Paste in "Additional Boards Manager URLs":
    ```
    https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
    ```
  - Tools → Board Manager → Search "ESP32" → Install

**Steps:**
```
1. Open NYX-Probe-Firmware/src/main.cpp in Arduino IDE
2. Tools → Board → Select "ESP32 Dev Module"
3. Tools → Port → Select your COM port
4. Tools → Upload Speed → 115200
5. Click Upload button (→ arrow icon)
6. Wait for "Leaving... Hard resetting via RTS pin" message
7. Open Serial Monitor (Tools → Serial Monitor) to verify boot
```

### Method 3: Web Installer (Easiest - No Installation)

If you just have the compiled `.bin` file:
```
1. Go to https://web.esptool.io/
2. Click "Connect"
3. Select your ESP32 COM port
4. Select the .bin file (address: 0x1000)
5. Click "Program"
6. Wait for success message
```

### Troubleshooting Upload Issues

| Problem | Solution |
|---------|----------|
| **"Device not found"** | Check USB cable, try different port, restart IDE |
| **"Permission denied"** | Run IDE as Administrator (Windows) or use `sudo` (Linux/Mac) |
| **"COM port not showing"** | Install CH340 driver or CP2102 driver (check your board) |
| **"Upload timeout"** | Lower baud rate to 115200, try different USB port |
| **"Out of memory"** | Check flash size (4MB minimum), reduce partition size |

---

## 〈 FIRST BOOT 〉

After successful flash:

1. **Connect Battery/Power**
   - Device will boot automatically
   - OLED should light up within 2 seconds
   - Main menu will appear

2. **Initial Configuration**
   - Brightness might be low (adjust in Settings)
   - Test all buttons (UP, DOWN, SELECT, BACK)
   - Verify OLED displays correctly

3. **Verify Modules**
   - WiFi should scan networks
   - BLE should find devices
   - GPS might take 2-5 minutes for first fix

4. **Run Diagnostics**
   - Main Menu → Device/System → Device Info
   - Check firmware version and module status
   - Verify storage space available

---

## 〈 CORE FEATURES 〉

### 🔍 WiFi Module (6 Main Features)

#### SCAN — Discover Networks
- **Active Scan** — Send probes, fast discovery
- **Passive Scan** — Listen only, stealthy mode
- **Hidden SSID** — Find cloaked networks
- **Channel Hop** — Scan all frequencies

**Output:** Network name, MAC address, channel, signal strength, security type

#### SNIFF — Monitor & Capture
- **Probe Sniffing** — Track device searches
- **Beacon Detection** — Monitor network broadcasts
- **Deauth Detection** — Identify disconnections
- **PMKID Capture** — Collect handshake data
- **Channel Analyzer** — Analyze frequency usage
- **Signal Monitoring** — Track RSSI strength
- **MAC Tracking** — Follow device movements
- **Raw Sniffing** — Capture all frames

**Output:** Real-time network activity, data logs, signal analysis

#### ATTACKS — Test Network Security
- **Beacon Spam** — Broadcast random networks
- **Rickroll Beacon** — Fun WiFi name
- **Probe Flood** — Overwhelm scanners
- **Deauth Target** — Disconnect specific device
- **Deauth Flood** — Disconnect all clients
- **AP Cloning** — Create fake access point
- **Karma Attack** — Respond to all probes
- **Channel Switch** — Force reconnections
- **Quiet Time** — Silent observation mode

**Output:** Test results, network response analysis, disruption logs

#### CONFIG — WiFi Settings
- **Set SSID** — Network name
- **Set Password** — Authentication
- **Set Channel** — Operating frequency
- **Monitor Mode** — Enable sniffing
- **Kill WiFi** — Disable all transmissions

---

### 📡 Bluetooth / BLE Module (3 Main Features)

#### BT Sniffing
- **Classic Bluetooth** — Legacy BT discovery
- **BLE Scan** — Low energy devices
- **iBeacon** — Apple proximity devices
- **Flipper Mode** — Alternative scan method

**Output:** Device name, MAC address, signal strength, proximity

#### BT Attacks
- **BLE Spam** — Flood advertisements
- **BT Jamming** — Disrupt connections
- **Device Spoofing** — Impersonate devices

**Output:** Attack status, interference metrics, connection logs

---

### 🌐 Network / IP Module (5 Scan Types)

- **ARP Scan** — Find local network devices
- **Port Scan** — Identify open services (100 ports, full range, custom, UDP)
- **SSH Scan** — Detect SSH services
- **Telnet Scan** — Find legacy services
- **Ping Scan** — Check host availability

**Output:** Active hosts, open ports, service identification, response times

---

### 🗺️ GPS Module (3 Features)

- **GPS Data** — Real-time position, altitude, speed, heading
- **GPS Tracker** — Log location history to storage
- **Wardrive** — Map WiFi networks with GPS locations
  - Start/stop logging
  - Export as KML (Google Earth)
  - View collected data

**Output:** Coordinates, altitude, movement history, network maps

---

### ⌨️ BLE HID Module (Attack Payloads)

#### Attacks
- **Rickroll Prank** — Opens browser rickroll
- **Typing Test** — Auto types text
- **Open Calculator** — Launches calc app

#### Keyboard Shortcuts
- **Alt + F4** — Close window
- **Win + D** — Show desktop
- **Alt + Tab** — Switch apps

#### Custom Payloads
- Create custom keystroke sequences
- Program any keyboard combination
- Automated macro execution

**Target:** Unlocked computers with BLE keyboard support

---

### 🔧 Device / System Module

- **Update Firmware** — Flash new version
- **Device Info** — Hardware specs, storage, battery
- **Settings** — Brightness, theme, calibration, factory reset
- **Reboot** — Restart device

---

## 〈 MENU NAVIGATION 〉

```
BUTTONS:
├─ UP/DOWN  → Navigate menu items (↑↓)
├─ SELECT   → Enter submenu / Start action (→)
└─ BACK     → Return to previous menu (←)

MAIN MENU STRUCTURE:
├─ 1. WIFI
│  ├─ SCAN       → Find networks
│  ├─ SNIFF      → Monitor traffic
│  ├─ ATTACKS    → Test security
│  └─ CONFIG     → Configure
│
├─ 2. Bluetooth / BLE
│  ├─ Scanning   → Find devices
│  ├─ Sniffing   → Monitor
│  └─ Attacks    → Test
│
├─ 3. Network / IP
│  ├─ ARP Scan   → Local devices
│  ├─ Port Scan  → Services
│  └─ Ping Scan  → Availability
│
├─ 4. GPS Features
│  ├─ GPS Data   → Position
│  ├─ Tracker    → Log location
│  └─ Wardrive   → Map networks
│
├─ 15. BLE HID
│  ├─ Status     → Connection
│  ├─ Attacks    → Payloads
│  ├─ Shortcuts  → Hot keys
│  └─ Custom     → User payloads
│
└─ 5. Device / System
   ├─ Update     → Flash firmware
   ├─ Info       → Device stats
   ├─ Settings   → Customize
   └─ Reboot     → Restart
```

---

## 〈 QUICK WORKFLOWS 〉

### Find Nearby WiFi Networks
```
Main Menu → WIFI → SCAN → Passive Scan
Wait 10-15 seconds → See network list
SELECT network for details
```

### Discover Local Network Devices
```
Main Menu → Network/IP → ARP Scan
Enter range (e.g., 192.168.1.1-254)
Wait for scan → See active devices with IP + MAC
```

### Check Open Ports on a Device
```
Main Menu → Network/IP → Port Scan
Select "Top 100 Ports"
Enter target IP → Wait for scan results
View open ports and services
```

### Find Bluetooth Devices
```
Main Menu → Bluetooth/BLE → BLE Scan
Wait 15-30 seconds → See nearby BLE devices
Shows device names, MAC, signal strength
```

### Map WiFi Networks with GPS (Wardriving)
```
1. Ensure GPS has satellite fix (2-5 minutes)
2. Main Menu → GPS → Wardrive → Start Log
3. Walk/drive around with device
4. Device logs WiFi + GPS location
5. Return to menu → Export KML
6. Open KML file in Google Earth to see map
```

---

## 〈 CONFIGURATION 〉

Edit `src/config.h` to customize:

```cpp
// GPIO Pins
#define OLED_SDA 21
#define OLED_SCL 22
#define BTN_UP 25
#define BTN_DOWN 26
#define BTN_SELECT 27
#define BTN_BACK 14

// WiFi Settings
#define WIFI_CHANNEL_DEFAULT 6
#define WIFI_POWER_MAX 20

// BLE Settings
#define BLE_SCAN_TIME 10
#define BLE_SCAN_INTERVAL 100

// GPS (if equipped)
#define GPS_BAUD_RATE 9600
#define GPS_ENABLED 1

// Features Enable/Disable
#define ENABLE_WIFI 1
#define ENABLE_BLE 1
#define ENABLE_NETWORK 1
#define ENABLE_GPS 1
#define ENABLE_HID 1

// Display
#define BRIGHTNESS_DEFAULT 150
#define DISPLAY_REFRESH_RATE 100

// Storage
#define SPIFFS_SIZE_MB 2
#define LOG_TO_STORAGE 1
```

---

## 〈 PROJECT STRUCTURE 〉

```
src/
├── main.cpp              # Entry point & main loop
├── config.h              # Configuration & pins
├── menu_system.cpp/h     # OLED menu interface
│
├── modules/
│   ├── wifi_module.cpp   # WiFi scanning & attacks
│   ├── ble_module.cpp    # Bluetooth/BLE operations
│   ├── network_module.cpp# ARP, port, ping scanning
│   ├── gps_module.cpp    # GPS & wardriving
│   ├── hid_module.cpp    # BLE HID attacks
│   └── system_module.cpp # Device management
│
├── ui/
│   ├── display.cpp       # OLED rendering
│   └── display.h
│
└── utils/
    ├── logger.cpp        # Data logging
    ├── helpers.cpp       # Utility functions
    └── data_storage.cpp  # SPIFFS file management
```

---

## 〈 TROUBLESHOOTING 〉

| Issue | Solution |
|-------|----------|
| **OLED not displaying** | Check I2C address (0x3C or 0x3D), verify SDA/SCL pins (21, 22) |
| **Buttons not responding** | Verify GPIO pins match config.h, test with digitalRead() |
| **WiFi scan slow/frozen** | Reduce scan duration, disable other modules, check RAM |
| **BLE not finding devices** | Ensure BLE enabled, wait longer (15-30s), check device is broadcasting |
| **GPS no fix** | Get clear sky view, wait 3-5 minutes, verify UART pins, check baud rate |
| **BLE HID not working** | Verify BLE enabled, test with BLE keyboard target, check pairing |
| **Battery drains quickly** | Reduce OLED brightness, disable unused modules, use larger battery |
| **Firmware won't upload** | Check USB cable, try different COM port, update board driver |
| **Memory errors** | Reduce buffer sizes, disable unused modules, recompile with optimizations |

---

## 〈 PERFORMANCE SPECS 〉

```
Boot Time:              2-3 seconds
WiFi Passive Scan:      10-20 seconds
WiFi Active Scan:       5-15 seconds
BLE Scan:               10-30 seconds
ARP Scan (/24):         2-5 seconds
Port Scan (100 ports):  30-60 seconds
Port Scan (1000 ports): 5-10 minutes
GPS Fix:                2-5 minutes first fix
Battery Life:           2-4 hours (continuous)
Storage:                ~4MB SPIFFS
Memory:                 ~80-90% used
```

---

## 〈 DATA FORMATS 〉

### Export Formats
- **CSV** — Spreadsheet (Excel, Google Sheets)
- **KML** — Google Earth mapping
- **JSON** — API compatible
- **RAW** — Binary capture

### Logged Data
- WiFi networks (SSID, BSSID, channel, RSSI)
- Connected devices (IP, MAC, status)
- GPS locations (latitude, longitude, altitude)
- BLE devices (name, MAC, RSSI)
- Scan results with timestamps

---

## 〈 SECURITY DISCLAIMER 〉

⚠️ **IMPORTANT NOTICE:**

NYX Probe is **ONLY** for authorized security testing, research, and educational purposes.

**Before Using:**
- ✅ Get explicit written permission from network/device owners
- ✅ Understand laws in your jurisdiction (CFAA, GDPR, local laws)
- ✅ Document authorization and testing scope
- ✅ Maintain detailed logs of activities

**PROHIBITED:**
- ❌ Unauthorized network access/testing
- ❌ Disrupting legitimate services
- ❌ Privacy violations or data theft
- ❌ Any illegal or unethical activities

**CONSEQUENCES:**
- Authors assume NO liability for misuse
- Unauthorized testing is illegal
- Responsible disclosure required for findings
- Follow ethical hacking code of conduct

---

## 〈 INSTALLATION ISSUES 〉

### Can't find COM port?
- Check Device Manager (Windows) or `ls /dev/ttyUSB*` (Linux)
- Install CH340 or CP2102 USB driver for your board
- Try different USB cables

### "Board not in sync" error?
- Hold GPIO0 to GND while uploading
- Press EN (reset) button during upload
- Try baud rate 115200

### Running out of memory?
- Disable unused features in config.h
- Reduce buffer/array sizes
- Remove debug serial output
- Compile with optimizations (-O2)

### GPS not getting fix?
- Move outside, away from buildings
- Wait 5+ minutes for first fix
- Check antenna connection
- Verify UART pins match config

---

## 〈 CONTRIBUTING 〉

Contributions welcome! Please:
1. Fork repository
2. Create feature branch (`git checkout -b feature/name`)
3. Commit changes (`git commit -m 'Add feature'`)
4. Push to branch (`git push origin feature/name`)
5. Open Pull Request

### Areas for contribution:
- Bug fixes and optimizations
- New attack vectors
- UI/UX improvements
- Hardware integrations
- Documentation improvements
- Test cases

---

## 〈 REFERENCES 〉

- [ESP32 Documentation](https://docs.espressif.com/projects/esp-idf/)
- [WiFi 802.11 Security](https://en.wikipedia.org/wiki/IEEE_802.11)
- [Bluetooth Specification](https://www.bluetooth.com/specifications/specs/)
- [OWASP Wireless Testing](https://owasp.org/www-community/attacks/Wireless_attacks)
- [Arduino ESP32 Core](https://github.com/espressif/arduino-esp32)

---

## 〈 SUPPORT 〉

- **Issues:** Report bugs on GitHub
- **Questions:** Use GitHub Discussions
- **Security:** Report privately to maintainer
- **Documentation:** See full specs in repository

---

<div align="center">

```
╔════════════════════════════════════════════════════════╗
║  LEGAL NOTICE                                          ║
╠════════════════════════════════════════════════════════╣
║  This tool is for AUTHORIZED testing only             ║
║  Unauthorized access = ILLEGAL                        ║
║  Users responsible for compliance with laws           ║
║  Use responsibly. Test ethically. Hack legally.       ║
╚════════════════════════════════════════════════════════╝
```

---

**Created by:** ArjunMP-sudo  
**License:** MIT  
**Status:** Active Development  
**Last Updated:** 2024

### Happy Hacking! 🎯

For security. By security. Through learning.

</div>
