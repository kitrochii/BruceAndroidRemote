<div align="center">

# BruceBLE
**Unofficial Android BLE Remote & Screen Mirror for Bruce Firmware**

[![Platform](https://img.shields.io/badge/Platform-Android%20%7C%20Web%20Bluetooth-a855f7?style=flat-square)](#)
[![Target](https://img.shields.io/badge/Hardware-LilyGO%20T--Embed%20CC1101-22c55e?style=flat-square)](#)
[![Release](https://img.shields.io/github/v/release/YOUR_USERNAME/BruceBLE?style=flat-square&color=3b82f6)](../../releases)
[![License: AGPL v3](https://img.shields.io/badge/License-AGPLv3-ef4444?style=flat-square)](LICENSE)

A lightweight remote and real-time screen mirroring client for **Lilygo T-Embed CC1101 with Bruce Firmware** over BLE. Control your device and view its live display directly from your Android phone without Wi-Fi and USB.

[Download Latest APK](../../releases/latest) • [Open Web App](#) • [Report Issue](../../issues)

</div>

---

## Screenshots

<p align="center">
  <img src="assets/screenshot-controls.png" width="260" alt="Remote Controls & Screen Mirror" />
  <img src="assets/screenshot-terminal.png" width="260" alt="BLE CLI Terminal" />
</p>

---

## Features

- **Real-Time Screen Mirroring (`320×170`)** — Parses Bruce's live stream of `TFT_eSPI` draw calls, bitmaps, and `RGB565` frames onto an HTML5 Canvas with pixel-perfect scaling and one-tap PNG screen capture.
- **Full Hardwareless Control** — Tactile D-Pad and auxiliary keys mapped to the LilyGO T-Embed CC1101 rotary encoder (`PREV/UP`, `NEXT/DOWN`), directional navigation, `OK/SELECT`, and `BACK/ESC`.
- **Long Press & Auto-Repeat** — Native support for hold actions (`long` / `hold`) with visual charge feedback and haptic vibration, plus directional auto-repeat while holding navigation keys.
- **Instant Screen Repaint** — Request an immediate screen redraw (`screen repaint`) at any time to synchronize the current display frame.
- **Interactive BLE CLI Terminal** — Send raw serial commands (`info`, `free`, `storage free`, `subghz`, etc.) and inspect real-time device logs with automatic BLE packet reassembly.
- **Dual BLE Stack Support** — Implements the native Bruce Serial UUID (`4371EC0B-...`) ported from `BruceDevices/App-IOS` with automatic fallback to the Nordic UART Service (`NUS`) and Battery Service (`0x180F`).

---

## Prerequisites

### 1. Enable BLE on Bruce (LilyGO T-Embed CC1101)
By default, the BLE Serial API is disabled in Bruce Firmware. Enable it on your device before pairing:
1. Open the main menu and go to **Config**.
2. Navigate to **Advanced**.
3. Select **Toggle BLE API** (make sure it is enabled).

> **Note:** Bruce truncates its BLE advertisement packet name to `Bruc` with Scan Response disabled. BruceBLE filters for the `Bruc` prefix automatically.

### 2. Android Permissions
- Enable **Bluetooth** and **Location Services** on your Android device (required by Android OS for BLE scanning).

---

## Installation & Usage

### Option 1: Android APK (Recommended)
1. Download the latest `.apk` from the [**Releases**](../../releases/latest) page and install it on your Android device.
2. Open **BruceBLE**, tap **Connect** in the top bar, and select your `Bruc` / `Bruce` device from the scanner dialog.

### Option 2: Web App (Chrome on Android)
1. Open the hosted GitHub Pages URL in **Google Chrome** on Android.
2. Tap **Connect** and pair with your device over Web Bluetooth.

---

## BLE Protocol Specification

| Service / Characteristic | UUID | Role |
| :--- | :--- | :--- |
| **Bruce Serial Service** | `4371ec0b-3d43-49f9-b731-7c72a4a7bb91` | Primary BLE Service |
| **Bruce Serial R/W/Notify** | `d555ed97-bf2a-4f46-b3eb-d1fcdd7325e9` | Bidirectional TX/RX + Draw Stream |
| **Nordic UART Service (NUS)** | `6e400001-b5a3-f393-e0a9-e50e24dcca9e` | Fallback UART Service |
| **Battery Service** | `0x180F` / `0x2A19` | Real-time battery percentage |

---

## Credits

- **[BruceDevices / Bruce Firmware](https://github.com/pr3y/Bruce)** — Firmware for ESP32-based security & RF platforms.
- **[BruceDevices / App-IOS](https://github.com/BruceDevices/App-IOS)** — Reference BLE UUIDs, packet framing, and screen draw-call mirroring architecture.

## License

This project is licensed under the **GNU Affero General Public License v3.0 (AGPL-3.0)** — see the [LICENSE](LICENSE) file for details.
